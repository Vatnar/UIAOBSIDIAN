
devcontainer.json (pass på bygge locally)
```json
"mounts": [

"source=/tmp/.X11-unix,target=/tmp/.X11-unix,type=bind,consistency=cached",

"source=/run/user/1000/pulse,target=/run/user/1000/pulse,type=bind,consistency=cached"

],

"containerEnv": {

"PULSE_SERVER": "unix:/run/user/1000/pulse/native",

"NO_AT_BRIDGE": "1"

},

"runArgs": [

"--device=/dev/snd"

],
```
legg til osdev i audio group, for lyd. DockerFile
``` bash
&& usermod -aG audio osdev \
```

Build, Execution, Deployment / CMake, set cmake options, (inni devcontainer, etter du har mounta)
```bash
-DCMAKE_C_COMPILER=/usr/local/bin/i686-elf-gcc
-DCMAKE_CXX_COMPILER=/usr/local/bin/i686-elf-g++
```
Også bare å lage run config

