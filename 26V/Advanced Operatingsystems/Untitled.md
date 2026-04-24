
# Paging and Syscall Bug Fixes

This document explains the bugs found and fixed in the Group 42 OS kernel related to paging and syscalls.

## Bug 1: Page Table Offset Error

**Location:** `src/kernel/paging.c`

**Symptom:** Kernel crash immediately after `enable_paging()`.

**Root Cause:** The second page table was at `0x109000`, but the code used:
```c
uint32_t* second_pt = &_page_tables + 256;  // WRONG!
```

Since `_page_tables` is a `uint32_t*`, adding 256 adds `256 * 4 = 1024` bytes, resulting in `second_pt = 0x108000 + 1024 = 0x108400` instead of `0x109000`. This corrupted the first page table and broke identity mapping.

**Fix:**
```c
uint32_t* second_pt = &_page_tables + 1024;  // CORRECT: 1024 * 4 bytes = 0x1000 offset
```

**Effect:** PDE[1] now correctly points to `0x109003` (the second page table at `0x109000` with Present+RW flags).

---

## Bug 2: Bitmap Location Not Identity-Mapped

**Location:** `include/kernel/pmm.h`

**Symptom:** Recursive page faults when `vmm_map_page()` was called from the page fault handler.

**Root Cause:** The PMM bitmap was located at `0x500000`, which was outside the identity-mapped region (`0x0-0x400000`). When `pmm_alloc_frame()` accessed the bitmap after paging was enabled, it caused a page fault.

**Fix:** Extended identity mapping in `init_paging()` to cover `0x400000-0x800000`:

```c
uint32_t* second_pt = &_page_tables + 1024;
for (int i = 0; i < 1024; i++) {
    second_pt[i] = (0x400000 + i * PAGE_SIZE) | PAGE_PRESENT | PAGE_RW;
}
page_directory[1] = ((uint32_t)second_pt) | PAGE_PRESENT | PAGE_RW;
```

**Effect:** The bitmap at `0x500000` is now properly mapped via PDE[1].

---

## Bug 3: Page Table Frames Not Reserved in PMM

**Location:** `src/kernel/pmm.c`

**Symptom:** Page table frames at `0x108000-0x109FFF` could be allocated by `pmm_alloc_frame()` and overwritten.

**Root Cause:** `pmm_init()` did not explicitly reserve the page directory and page table frames.

**Fix:** Added explicit reservation in `pmm_init()`:

```c
uint32_t pgdir_frame = 0x00104000 / PMM_BLOCK_SIZE;    // 0x104
uint32_t pgtables_frame = 0x00108000 / PMM_BLOCK_SIZE; // 0x108

// Reserve page directory
if (pgdir_frame < num_frames) {
    pmm_info.bitmap[pgdir_frame / 8] |= (1 << (pgdir_frame % 8));
}

// Reserve page tables (2 frames)
for (uint32_t f = pgtables_frame; f < pgtables_frame + 2; f++) {
    if (f < num_frames) {
        pmm_info.bitmap[f / 8] |= (1 << (f % 8));
    }
}
```

**Effect:** Page table frames can no longer be allocated for other purposes.

---

## Bug 4: Syscall Stub Declared as Pointer Instead of Function

**Location:** `include/arch/i386/cpu/isr.h`

**Symptom:** `int 0x80` caused a page fault at address `0x8068006a` instead of reaching the syscall handler.

**Root Cause:** The declaration was:
```c
extern void* syscall_stub;  // WRONG: declares a pointer variable
```

But `syscall_stub` is a function label in `interrupts.asm`. The compiler treated it as a pointer variable, and the address `0x8068006a` suggests it was reading the function's first bytes as a pointer.

**Fix:**
```c
extern void syscall_stub(void);  // CORRECT: declares a function
```

**Effect:** The IDT gate 0x80 now correctly stores the address of `syscall_stub` (e.g., `0x10d8b7`).

---

## Bug 5: Syscall Register Passing (registers_t Layout)

**Location:** `include/arch/i386/cpu/isr.h` and `src/arch/i386/cpu/interrupts.asm`

**Symptom:** Syscall arguments (ebx, ecx, edx, etc.) arrived in wrong order or wrong values.

**Root Cause:** The `registers_t` struct didn't match the actual stack layout after `pushad` and the syscall stub's `push ds`. Also, the stub was saving ESP after modifying the stack.

**Fix:** 
1. Updated `registers_t` to match pushad order:
```c
typedef struct {
  uint32_t edi, esi, ebp, esp_pusha, ebx, edx, ecx, eax;
  uint32_t ds;
  uint32_t int_no, err_code;
  uint32_t eip, cs, eflags, esp, ss;
} registers_t;
```

2. Fixed syscall_stub to save ESP before modifying the stack:
```asm
global syscall_stub
syscall_stub:
    CLI
    PUSH 0
    PUSH 0x80
    PUSHA
    mov ebx, esp        ; Save ESP BEFORE pushing ds
    mov ax, ds
    push eax
    mov ax, 0x10
    mov ds, ax
    mov es, ax
    mov fs, ax
    mov gs, ax
    push ebx            ; Push saved ESP (points to pushad registers)
    cld
    call syscall_handler
    add esp, 4
    pop eax             ; Restore registers
    mov ds, ax
    mov es, ax
    mov fs, ax
    mov gs, ax
    POPA
    add esp, 8
    iret
```

3. Updated `syscall_handler` to read arguments correctly:
```c
args.number = regs->eax;
args.a = regs->ebx;
args.b = regs->ecx;
args.c = regs->edx;
args.d = regs->esi;
args.e = regs->edi;
args.f = regs->esp_pusha;
```

**Effect:** All syscall arguments now arrive correctly via `int 0x80`.

---

## Memory Layout Summary

After fixes, the identity-mapped memory regions are:

| Virtual Range | Physical Range | Purpose |
|--------------|----------------|---------|
| `0x00000000-0x003FFFFF` | Same (PDE[0], PT[0]) | Identity-mapped via first page table |
| `0x00400000-0x007FFFFF` | Same (PDE[1], PT[1]) | Identity-mapped via second page table |
| `0x00104000` | `0x00104000` | Page Directory |
| `0x00108000-0x00108FFF` | `0x00108000` | First Page Table (PT[0]) |
| `0x00109000-0x00109FFF` | `0x00109000` | Second Page Table (PT[1]) |
| `0x00100000-0x001FFFFF` | Same | Kernel text and data |

---

## Testing

After the fixes, the kernel boots and runs:
1. **Syscall test**: Calls `int 0x80` with `SYS_getpid` (syscall 20) and verifies return value
2. **Page fault test**: Writes to `0x10000` to test demand mapping
3. **Shell**: Starts an interactive shell where you can type `test_syscalls` to test syscall handlers directly

---

## Files Modified

1. **`src/kernel/paging.c`**
   - Fixed `second_pt` offset from `+256` to `+1024`
   - Added PDE[1] setup for `0x400000-0x800000`

2. **`src/kernel/pmm.c`**
   - Added reservation of page directory and page table frames

3. **`include/arch/i386/cpu/isr.h`**
   - Changed `extern void* syscall_stub` to `extern void syscall_stub(void)`
   - Updated `registers_t` struct to match pushad order

4. **`src/arch/i386/cpu/interrupts.asm`**
   - Fixed syscall_stub to save ESP before modifying stack
   - Now uses same register saving pattern as IRQ handlers

5. **`src/shell/commands/test_syscalls.c`**
   - Added comprehensive syscall tests via `int 0x80`
   - Added `syscall_via_int0x80()` helper with correct register passing

---

## Debug Techniques Used

1. **Serial debug output** via `out 0xE9, al` to trace execution flow
2. **Page fault handler diagnostics** to see fault address, error code, and EIP
3. **Unique register values test** - set unique values in registers and verify they arrive correctly

Key lessons:
- When an interrupt handler address looks like a data address (e.g., `0x8068006a`), check for type mismatches between function labels and their declarations
- When passing registers to inline asm, use constraint letters directly (`"a"`, `"b"`, `"c"`, `"d"`, `"S"`, `"D"`) rather than numbered `"r"` when possible
- The stack layout after `pushad` + extra pushes must exactly match the struct layout used to read it

