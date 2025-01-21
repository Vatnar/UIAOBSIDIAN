<h1>IKT102 Exam Study Plan and Topics</h1>

<h2>📅 Study Plan (22/11–26/11)</h2>

<div class="callout">
    <strong>Day 1: 22/11</strong><br>
    <strong>Focus:</strong> Processes, Threads, and Concurrency Issues<br>
    <ul><s>
        <li>Review the process lifecycle: <ul>
            <li>Creation, execution, termination.</li>
            <li>Segmentering</li>
        </ul></li>
        </s>
        <li>Study synchronization problems: <ul>
            <li>Race conditions</li>
            <li>Critical sections</li>
        </ul></li>
        <li>Learn key synchronization mechanisms: <ul>
            <li>Semaphores</li>
            <li>Mutexes</li>
            <li>Monitors</li>
        </ul></li>
        <li>Practice: Solve the Producer-Consumer problem.</li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Day 2: 23/11</strong><br>
    <strong>Focus:</strong> CPU Scheduling + Deadlocks<br>
    <ul>
        <li><strong>Scheduling algorithms:</strong>
            <ul>
                <li>First-Come-First-Serve (FCFS)</li>
                <li>Shortest Job Next (SJN)</li>
                <li>Priority Scheduling</li>
                <li>Round Robin (RR)</li>
            </ul>
        </li>
        <li>Calculate: <ul>
            <li>Turnaround time</li>
            <li>Waiting time</li>
            <li>Response time</li>
        </ul></li>
        <li><strong>Deadlocks:</strong>
            <ul>
                <li>Understand the four conditions for deadlock.</li>
                <li>Study avoidance strategies like the Banker’s Algorithm.</li>
                <li>Prevention and detection techniques.</li>
            </ul>
        </li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Day 3: 24/11</strong><br>
    <strong>Focus:</strong> Memory Management<br>
    <ul>
        <li>Memory allocation: <ul>
            <li>Paging</li>
            <li>Segmentation</li>
            <li>Virtual memory</li>
        </ul></li>
        <li>Concepts: <ul>
            <li>Page faults</li>
            <li>TLB (Translation Lookaside Buffer)</li>
            <li>Swapping</li>
        </ul></li>
        <li>Practice: Solve problems on paging and memory calculations.</li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Day 4: 25/11</strong><br>
    <strong>Focus:</strong> File Systems + I/O Management<br>
    <ul>
        <li><strong>File systems:</strong> 
            <ul>
                <li>File allocation methods: Contiguous, linked, indexed</li>
                <li>Directory structures: Single-level, two-level, hierarchical</li>
            </ul>
        </li>
        <li><strong>I/O management:</strong>
            <ul>
                <li>Buffering, caching, and spooling</li>
                <li>Device drivers and their role</li>
            </ul>
        </li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Day 5: 26/11</strong><br>
    <strong>Focus:</strong> Full review and problem-solving<br>
    <ul>
        <li>Solve problems on:
            <ul>
                <li>Scheduling algorithms</li>
                <li>Deadlock avoidance</li>
                <li>Paging/virtual memory</li>
            </ul>
        </li>
        <li>Review:
            <ul>
                <li>Key diagrams (e.g., process states, memory layouts)</li>
                <li>Summary notes for quick recall</li>
            </ul>
        </li>
    </ul>
</div>

<hr>

<h2>📚 Topics to Cover for the Exam</h2>

<div class="callout">
    <strong>Chapter 1: Overview of Operating Systems</strong><br>
    <ul>
        <li>What is an operating system?</li>
        <li>Responsibilities of an operating system:
            <ul>
                <li>Extended machine</li>
                <li>Resource manager</li>
                <li>User interface</li>
            </ul>
        </li>
        <li><strong>Structures:</strong>
            <ul>
                <li>Monolithic system</li>
                <li>Microkernel system</li>
                <li>Layered system (optional)</li>
                <li>Virtual machines (optional)</li>
                <li>Exokernels (optional)</li>
                <li>Client-server systems</li>
            </ul>
        </li>
        <li>32-bit vs. 64-bit systems.</li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Processes and Threads</strong><br>
    <ul>
        <li>Processes: Creation, use, termination.</li>
        <li>Threads: Creation, use, termination.</li>
        <li>PCB (Process Control Block) and context switching.</li>
        <li>System calls.</li>
        <li>Process/thread states: Ready, blocked, running, etc.</li>
        <li>User mode vs. kernel mode.</li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>CPU Scheduling</strong><br>
    <ul>
        <li>Batch, interactive, and real-time scheduling.</li>
        <li><strong>Algorithms:</strong>
            <ul>
                <li>Round-robin</li>
                <li>Priority scheduling</li>
                <li>Multiple queues</li>
                <li>Shortest Process Next</li>
                <li>Guaranteed Scheduling</li>
                <li>Lottery Scheduling</li>
                <li>Fair Share Scheduling.</li>
            </ul>
        </li>
        <li>I/O-bound vs. CPU-bound processes.</li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Inter-Process Communication (IPC)</strong><br>
    <ul>
        <li><strong>Classic problems:</strong>
            <ul>
                <li>Producer-consumer</li>
                <li>Readers-writers</li>
            </ul>
        </li>
        <li>Key concepts:
            <ul>
                <li>Atomic operations</li>
                <li>Race conditions</li>
                <li>Critical regions</li>
            </ul>
        </li>
        <li><strong>Synchronization tools:</strong>
            <ul>
                <li>Busy waiting</li>
                <li>Sleep and wake-up</li>
                <li>Semaphores</li>
                <li>Mutexes</li>
                <li>Monitors</li>
                <li>Message passing</li>
                <li>Barriers</li>
            </ul>
        </li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Deadlocks</strong><br>
    <ul>
        <li>Definition and conditions.</li>
        <li>Preemptable vs. non-preemptable resources.</li>
        <li>Deadlock handling:
            <ul>
                <li>Ostrich algorithm</li>
                <li>Detection</li>
                <li>Avoidance (e.g., Banker's Algorithm)</li>
                <li>Prevention</li>
            </ul>
        </li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>Memory Management</strong><br>
    <ul>
        <li>Basics of memory:
            <ul>
                <li>Mono-programming (without swapping or paging)</li>
                <li>Multiprogramming</li>
            </ul>
        </li>
        <li>Relocation and protection.</li>
        <li>Memory hierarchy.</li>
        <li>Addressing:
            <ul>
                <li>Relative, absolute, physical</li>
            </ul>
        </li>
        <li>Swapping:
            <ul>
                <li>Bitmaps, linked lists</li>
            </ul>
        </li>
        <li><strong>Virtual memory:</strong>
            <ul>
                <li>Paging and page tables</li>
                <li>Page replacement algorithms:
                    <ul>
                        <li>Optimal</li>
                        <li>Not Recently Used (NRU)</li>
                        <li>FIFO</li>
                        <li>Second-chance</li>
                        <li>Clock</li>
                        <li>Least Recently Used (LRU)</li>
                        <li>Working set</li>
                        <li>Aging</li>
                    </ul>
                </li>
            </ul>
        </li>
        <li>Segmentation:
            <ul>
                <li>Paging and segmentation together</li>
                <li>X86 segmentation</li>
            </ul>
        </li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>I/O Management</strong><br>
    <ul>
        <li><strong>Hardware/software layers:</strong>
            <ul>
                <li>I/O devices</li>
                <li>Device controllers</li>
                <li>Memory-mapped I/O</li>
                <li>DMA (Direct Memory Access)</li>
            </ul>
        </li>
        <li>Interrupt handling and device drivers.</li>
        <li><strong>Disk scheduling:</strong>
            <ul>
                <li>Arm disk scheduling algorithms</li>
                <li>Error handling</li>
            </ul>
        </li>
    </ul>
</div>

<hr>

<div class="callout">
    <strong>File Systems</strong><br>
    <ul>
        <li><strong>Types of file systems:</strong>
            <ul>
                <li>FAT (File Allocation Table)</li>
                <li>Ext (Extended File System)</li>
            </ul>
        </li>
        <li><strong>File system structure:</strong>
            <ul>
                <li>File allocation methods</li>
                <li>Directory structure</li>
                <li>File types and operations</li>
            </ul>
        </li>
        <li><strong>File system implementation:</strong>
            <ul>
                <li>Log-structured file systems</li>
                <li>Journaling file systems</li>
            </ul>
        </li>
    </ul>
</div>

