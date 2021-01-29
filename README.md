# raspberryPi_pico

A repository of an example how to use RaspberryPi Pico as a submodule.
The specific steps are elaborated below.

## Write the code

Write the code in `src/main.c`

## Build the code

```bash
mkdir -p ${PROJECT_DIRECTORY}/build
cd ${PROJECT_DIRECTORY}/build
cmake ..
make main
```

## Debug the code

A `main.elf` file will be made in the `build` directory.
Use it to debug the program.

## Move the code (to RPi)

Move the main.uf2 to the RaspberryPi Pico.
