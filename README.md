# CMSIS STM32L4 Makefile template project

I was struggling to find a CMSIS Makefile project for STM32L4 devices.
This code is working (simple led blink) on PB3 GPIO (LED LD3 of Nucleo L412KB board).

The linker script is the one generated by STM32Cube IDE.
The CMSIS part is from [STM32CubeL4 repository](https://github.com/STMicroelectronics/STM32CubeL4).
The CFLAGS are also extracted from STM32Cube IDE Makefiles.

What I have done is put everything together for a simple use with VSCode, make and gdb.

## Prerequisites

- [GNU Arm Embedded Toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads), I extracted the toolchain in /opt/arm-none-eabi/10-2020-q4. The template is made for this path
- OpenOCD
- [VSCode](https://code.visualstudio.com)
-  VSCode Extensions (Optional):
   - [Cortex-debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug)
   -  [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

## Build

Simply run `make` to generate the elf and bin file.
A debug version is available (optimisations `-O0` and `-g` flag for GDB), run `make debug`

Tasks can also be used to generate the binaries.

## Flash

Simply run `make flash` to flash your device.

## Debug

VSCode only: Start the debugging task by pressing F5. Two debug configurations are possible, one in Release, one in Debug.

## Change the default device

You will first need to change/modify/update the linker script. You can use one generated by STM32CudeIDE or modify the `MEMORY` zone.

You will need to change some parameters:

- In the Makefile:
  - `LDFILE` will indicate your new device   linker script
  -  `DEVICE` will indicate the device name. Refer to `CMSIS/Device/ST/STM32L4xx/Include/stm32l4xx.h` for the device list
  - `CMSIS_SYS_SRC` will indicate the `system_stm32l4*.c` file in CMSIS
  - `CMSIS_START_SRC` will indicate the `startup_stm32l4*.s` file in CMSIS
- in the `.vscode` folder:
  - `svdFile` in the `.vscode/launch.json` will indicate the SVD file matching your device

## FAQ

**My debugger stops when I start it (but OpenOCD stays open)**
A ncurses library was needed for gdb to work correctly :`ncurses-compat-libs`, install it and try again.

## Disclamer

The code within this repository comes with no guarantee, the use of this code is your responsibility.

I take NO responsibility and/or liability for how you choose to use any of the source code available here. By using any of the files available in this repository, you understand that you are AGREEING TO USE AT YOUR OWN RISK.
