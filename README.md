# Watchdog Example

* The following guide describes how you can use the watchdog timer on the XMC.
* The wadchdog timer is not supported by default from mbed. So this guide also shows how you can write classes to support XMC hardware which has no mbed support.
* Check out this tutorial which descibes how you can write your own librarys. [LINK](https://os.mbed.com/cookbook/Writing-a-Library)
* An XMC Watchdog library is available here: [LINK](https://github.com/mbed-Infineon-XMC/XMCWatchdog-Library.git)

The watchdog timer is configured to 5s. If wd.service() is not called at least once during this period, the watchdog timer will reset the microcontroller.
In this example wd.service() is called every second. (LED 2 blink)
If button2 is pressed the wadchdog timer expired because wd.service() is not longer called and the XMC will reset after 5 seconds.
At the next start the XMC ckecks with wd.watchdogCauseReset() if the watchdog timer was the cause of reset an LED1 turns on.

## Step 1: Download mbed CLI

* [Mbed CLI](https://docs.mbed.com/docs/mbed-os-handbook/en/latest/dev_tools/cli/#installing-mbed-cli) - Download and install mbed CLI.

## Step 2: Import Watchdog-Example project

Import Watchdog-Example project from GitHub.

```
mbed import https://github.com/mbed-Infineon-XMC/Watchdog-Example.git
```

## Step 3: Install ARM GCC toolchain

* [GNU ARM toolchain](https://launchpad.net/gcc-arm-embedded) - Download and install the last stable version of the ARM GCC toolchain.
* Open the file "mbed_settings.py" and add the ARM GCC install path.

Example:
```
#GCC_ARM_PATH = "home/bin/arm_gcc_toolchain/gcc-arm-none-eabi-5_4-2016q2/arm-none-eabi/bin"
```
## Step 4: Import XMC Watchdog library

```
cd Watchdog-Example.git/
mbed add https://github.com/mbed-Infineon-XMC/XMCWatchdog-Library.git
```

## Step 5: Compile project

Navigate into the project folder and execute the following command:
```
mbed compile -m XMC_4500_RELAX_KIT -t GCC_ARM
```
mbed creates a BUID directory where you can find the executables (bin, elf, hex ...).

## Step 6: Flash to board

* [Segger JLink](https://www.segger.com/downloads/jlink) - Install the JLink software for your platform.
* Navigate to the BUILD directory and execute the following JLinkExe commands.
```
$ JLinkExe
J-LINK> device xmc4500-1024
J-LINK> h
J-Link> loadfile Watchdog-Example.git.hex
J-Link> r
J-Link> g
```
* Choose SWD, 4000kHz as interface settings!!
