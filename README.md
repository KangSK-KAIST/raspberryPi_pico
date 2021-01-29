# raspberryPi_pico

A repository of an example how to use RaspberryPi Pico as a submodule.
The specific steps are elaborated below.

Note that `${PROJECT_DIRECTORY}` is the root directory of the cloned version of this repository.

## Prerequisites

Run the following command to install all programs needed.

```shell
sudo apt install cmake doxygen gcc-arm-none-eabi libnewlib-arm-none-eabi
```

## Initialize the repository

Run the following command.

```shell
cd ${PROJECT_DIRECTORY}
git submodule update --init --recursive
```

## Write the code

Write the code in `src/main.c`

## Build the code

Run the following command.

```shell
mkdir -p ${PROJECT_DIRECTORY}/build
cd ${PROJECT_DIRECTORY}/build
cmake ..
make main
```

## Debug the code

A `main.elf` file will be made in the `build` directory.
Use it to debug the program.

## Move the code (to RPi)

Move the `main.uf2` to the RaspberryPi Pico.

## Additional Resources

For more information, please visit the original repo below.
https://github.com/raspberrypi/pico-sdk.git
