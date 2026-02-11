```bash
-DCMAKE_C_COMPILER=/usr/local/bin/i686-elf-gcc
-DCMAKE_CXX_COMPILER=/usr/local/bin/i686-elf-g++
```

devcontainer.json
```json
////////////////////////////////////

// Linux Setup (X11)

////////////////////////////////////

"mounts": [

"source=/tmp/.X11-unix,target=/tmp/.X11-unix,type=bind,consistency=cached",

],

"containerEnv": {},

"runArgs": [

"--device=/dev/snd"

],
```