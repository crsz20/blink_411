# blink_411

An Blinky LED example program for testing your local VSCode environment in tandem with stm32CubeIDE.

## Before You Start
- Install the following dependencies:
  - stm32CubeCLT (requires `Make` & stm32CubeIDE) — Flashing/erasing the program on the dev board's flash memory.
  - `CMake` (not to be confused with `Make`) — Compiling.
  - VSCode extensions
    - Embedded Tools by Microsoft — Viewing processor registers, RTOS data viewer, etc.
    - C/C++ by Microsoft — Syntax highlighting.
    - CMake Tools by Microsoft — a build generator. Note that the STM32 extension also installs Ninja. That is, CMake is leveraging Ninja to perform the compilation and linking, instead of Make.
    - GNU Linker Map Files
    - Arm Assembly
   
## Opening the Project
- Open VSCode after cloning this repo.
- Under the stm32 extension, import the project's `.cproject` file
- The package manager, `vcpackage` will immediately start to configure CMake and Ninja for compiling the program.
- Select a build preset for CMake to use. `Release` is the most optimized for performance and reduced size of the resulting binaries. However, we cannot debug. So, for development, use the `Debug` preset. 
- Now, let's build and flash

---

## Compiling
### Method 1: Using GUI Buttons
- Under the CMake extension, click the ellipsis button to **clean** the project. This is removing any lingering binaries and executables from previous builds.

![image](https://github.com/crsz20/blink_411/assets/71054319/66d46963-44b8-4283-87a2-95b523ff7e8d)

- Under the CMake extension, click on the **build** button.

![image](https://github.com/crsz20/blink_411/assets/71054319/76c387a7-8fad-483a-a9ff-af764d9bda21)

- You should be able to see the output of building/compiling in the `./build/debug/build` directory.
- You will find the following important files: `.bin`, .`hex`, and `.elf` (Executable Linker File). Any one of these files can be used to flash the dev board.


### Method 2: Using the Command Line
- Open the terminal
- At the project's root directory, run the following command: `cmake --build ./build/debug/build --target blink_f411`
- If you pay attention to the console output in the GUI method, this exact same command is used.

### Method 3: Using a Pre-Configured VSCode "Task"
- Assuming a Windows platform, press `ctrl+p`
- Type `task`
- Select `Build`
- This task is defined in the `.vs/tasks.json` file 

---

## Flashing
### Method 1: Debugging
- Launch the debugger

![image](https://github.com/crsz20/blink_411/assets/71054319/80fe60fb-b783-44f1-9fd8-278cc7eff03f)


### Method 2: Using CubeCLT
- Open the terminal
- At the project's root directory, run the following command: `STM32_Programmer_CLI -c port=SWD -w ./build/debug/build/blinkf411.elf 0x08000000`
- This command is enabling SWD for programming, and writing to the started address of the "code region" in flash memory (namely, `0x08000000`)

### Method 3: Using a Pre-Configured VSCode "Task"
- Assuming a Windows platform, press `ctrl+p`
- Type `task`
- Select `Flash`
- This task is defined in the `.vs/tasks.json` file 
