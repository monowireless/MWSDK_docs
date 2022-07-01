---
title: "Building ACT"
author: "Mono Wireless Inc."
description: "Building ACT"
---

# Building ACT

The application program written in the MWX library is called ACT. The first step is to build and write it.

* About the build directory structure
* About the build script
* About building with VS Code

{% hint style="info" %}
This page describes several methods of building, all of which ultimately involve running the make command. Please refer to the [Makefile description](makefile.md) for details.
{% endhint %}



## About the build directory structure

Open the directory `MWSDK_ROOT` (e.g. `C:\MWSDK`) where you have installed the MWSDK. It has the following structure

```
MWSDK_ROOT
  |
  +-ChipLib      : Semiconductor library
  +-License      : Software License Agreement
  +-MkFiles      : makefile
  +-Tools        : A set of tools such as compilers
  +-TWENET       : TWENET/MWX library
  +-Act_samples  : Sample codes of ACT
  ...
```



Tool act files such as compilers are stored under `Act_samples`. (Some of them are omitted below)

```
Act_samples
  |
  +-BRD_APPTWELITE    : ACT for boards with the same configuration as App_TweLite
  +-PAL_AMB           : ACT for environmental sense PAL
  +-PAL_MAG           : ACT for open-close PAL
  +-PAL_MOT           : ACT for motion PAL
  ..
  +-Parent-MONOSTICK  : ACT for parent device (for MONOSTICK)
  +-PingPong          : ACT for transmit and receive like Ping Pong
  +-PulseCounter      : ACT using a pulse counter
  +-act0              : Scratching ACT
```

These acts are simple examples to help you write your own MWX library, but many of them have the following features

* Obtaining sensor values
* After obtaining the sensor value, send a wireless packet to the master
* Sleeps for a period of time (or waits for an interrupt) after transmission is complete

The Parent-MONOSTICK act is used to receive and display packets. This act for the parent is output in ASCII format. (`:00112233AABBCC.... .FF[CR][LF]`, and the middle part is a hexadecimal byte expressed by two ASCII characters. The trailing ? is also a two-character byte, but it becomes a checksum byte called LRC. Reference: ASCII format)

When trying to get it to work in practice, try the following combinations:

| Parents                                                  | Child                                                 | Remark                                                                                                                                 |
| -------------------------------------------------------- | ----------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| [BRD\_APPTWELITE](../act\_samples/brd\_apptwelite.md)    | [BRD\_APPTWELITE](../act\_samples/brd\_apptwelite.md) | The parent device is started with the M1 pin low (GND level). In normal mode (always running), you can see it works like App\_TweLite. |
| [PingPong](../act\_samples/pingpong.md)                  | [PingPong](../act\_samples/pingpong.md)               | The system works with two children. When one of them sends a ping packet, the other sends a pong packet back.                          |
| [Parent-MONOSTICK](../act\_samples/parent\_monostick.md) | Other                                                 | You can check the transmission of packets of the act for the child machine.                                                            |



Now let's take a look inside the PingPong directory from within ACT.

{% hint style="info" %}
You can also build other acts in `Act_samples`. In this case, the directory and file names should be read differently.
{% endhint %}

```
Act_samples
  +-PingPong
    +-PingPong.cpp   : ACT code
    +-build          : build directory
    +-.vscode        : setting files for VS Code
```

You must have a `.cpp` file with the same name as the directory directly under the directory.

{% hint style="info" %}
If it is a small act, you can write it in this `.cpp` file. If you have a larger act, you can build it in multiple files by referring to the [Makefile description](makefile.md).
{% endhint %}

{% hint style="warning" %}
The ACT file PingPong.cpp is located directly under the PingPong directory. If you change the name of the directory, make sure to rename the .cpp file to the same name as the directory.
{% endhint %}



Next, open the build directory.

```
Act_samples
  +-PingPong
    +-build
      +-Makefile        : makefile
      +-build-BLUE.cmd  : build script for TWELITE BLUE
      +-build-RED.cmd   : build script for TWELITE RED
      +-build-clean.cmd : clean up obj_* files
```

It contains the scripts and Makefiles needed for the build.



## Build Script (Windows 10)

{% hint style="warning" %}
On macOS and Linux, you can build using VS Code or the command line.
{% endhint %}

Build scripts are suitable for completed ACTs, sample offerings, etc., which are less prone to errors.

The following is a script (batch file) for Windows 10.

| Name           | Remark           |
| -------------- | ---------------- |
| build-BLUE.cmd | for TWELITE BLUE |
| build-RED.cmd  | for TWELITE RED  |

After execution, a `bin` file will be created and will contain `PingPong_BLUE_???.bin` or `PingPong_RED_???.bin`. The `???`will be replaced by the version number or library version letter.

![PingPong アクトのディレクトリを開く](<../.gitbook/assets/image (23).png>)

![Double-click on build-BLUE.cmd (Run)](<../.gitbook/assets/image (24).png>)

![ビルド結果](<../.gitbook/assets/image (22).png>)

![A BIN file (PingPong\_BLUE\_L1203\_V0-1-0.bin) has been created.](<../.gitbook/assets/image (25).png>)



{% hint style="success" %}
If a BIN file is created, the build is successful.
{% endhint %}

{% hint style="info" %}
The `objs_BLUE` directory is an intermediate file generated during the build process. You can delete it if you wish.
{% endhint %}

{% hint style="warning" %}
In order to speed up the build, we have set up a parallel build option. This makes it difficult to see the error messages in case of errors.

If you want to see the error messages efficiently, we recommend using a development tool such as VS Code.
{% endhint %}



### Clean (remove intermediate files)

If you run `build-clean.cmd`, it will clean directories starting with `objs_`, but not BIN files.

{% hint style="warning" %}
If the build does not work, check the error messages first; often the cause of the error can be easily identified from a message on a line containing the string error.

Delete the intermediate files in the `objs_?` directory and try running it again. (All operations, including `make clean`, will fail if there are any intermediate files left over from builds in other environments).
{% endhint %}

## Build on command line (Linux/macOS)

Additional information about building in the command line environment.

{% hint style="warning" %}
A working knowledge of the command line (bash) is required.
{% endhint %}

{% hint style="danger" %}
Depending on the OS environment, security warnings may appear when running each executable program. It is necessary to configure the settings to suppress the warning. (**Please consult with yourself or your system administrator to determine if you wish to run the program with the warning suppressed.**)
{% endhint %}



To build by command line, run `make` in a window where `bash` (Bourne-again shell) is running. Make sure that the environment variable `MWSDK_ROOT` is set correctly beforehand. For example, if you install to `C:/MWSDK`, set `~/.profile` as follows.

```bash
MWSDK_ROOT=/mnt/c/MWSDK
export MWSDK_ROOT
```



Run `make` from the command line (bash). If `make` is not available, you need to install a package.

```bash
$ make

Command 'make' not found, but can be installed with:

sudo apt install make
sudo apt install make-guile

$ sudo apt install make
...
```

{% hint style="info" %}
* On Linux/WSL environments, install the `make` or `build-essential` package.
* In the macOS environment, install Command Line Tools in Xcode.
{% endhint %}



A build should look like this:

```
$ cd $MWSDK_ROOT
$ cd Act_samples/PingPong/build
$ pwd
/mnt/c/MWSDK/Act_samples/PingPong/build

$ ls
... View file list

$ rm -rfv objs_*
... Delete intermediate files just in case

$ make TWELITE=BLUE
... Normal build for BLUE

$ make -j8 TWELITE=BLUE
... Parallel build for BLUE (8 processes simultaneously)
```



### About intermediate files

When the build is done, the `objs_???` directory is created and an intermediate file is created in it. This file is dependent on the environment in which it was compiled, so if any files from other environments are left, make will fail and the build will fail.

{% hint style="warning" %}
If `make` fails, directly **delete** the `objs_???` directory.
{% endhint %}



### Example commands

See the [Makefile description](makefile.md) for more details.

| Example             | Remark                    |
| ------------------- | ------------------------- |
| `make TWELITE=BLUE` | build for TWELITE BLUE    |
| `make TWELITE=RED`  | build for TWELITE RED     |
| `make cleanall`     | Delete intermediate files |



## About building with VS Code

{% hint style="danger" %}
TWELITE STAGE is recommended for builds.

The VS Code definition files for the sample projects supplied with the MWSDK are implemented as far as possible, but some definitions could be incomplete.
{% endhint %}

{% hint style="danger" %}
Depending on the OS environment, security warnings may appear when running each executable program. It is necessary to configure the settings to suppress the warning. (Please consult with yourself or your system administrator to determine if you wish to **run the program with the warning suppressed.**)
{% endhint %}

In VS Code, you can either open the workspace file directly under the `Act_samples` directory, or open the act directory under `Act_samples`.

{% hint style="warning" %}
In the example below, a workspace is opened with an example screen of the English interface.
{% endhint %}

Open a workspace and select `[Terminal>Run Task...]`.

![List of build tasks](<../.gitbook/assets/image (1).png>)



Select the type of TWELITE radio module (BLUE/RED) and the act name to build. In the example below we have selected Build for TWELITE BLUE PingPong (for TWELITE BLUE/PingPong act). The build will start immediately after selection.

![Selecting a build task](<../.gitbook/assets/image (3).png>)



The progress of the build is shown in the TERMINAL section at the bottom of the screen.

![Build progress](<../.gitbook/assets/image (20).png>)

{% hint style="success" %}
If the build is successful, you will see a message about the creation of the `.elf` file, along with its size information (`text data bss dec hex filename`), as shown in the highlighted part of the screenshot above.

Also, a BIN file (in the above example, `PingPong_BLUE_???.bin`) file should be created under the `build` directory. Please check it.
{% endhint %}

{% hint style="info" %}
The build definition adds a definition to convert directory names (e.g. `/c/User/...`) that do not conform to the Windows 10 file system (e.g. `C:/User/...`).

The conversion is not complete, but you can extract the filename and line number of the error from the compilation message.

The execution command in `.vscode/tasks.json` is `sh -c "make ... | sed -E -e s#..."` to rewrite the string of the drive name equivalent in the output message.

```
...
"windows": {
    "command": "sh",
    "args": [
        "-c", "make TWELITE=BLUE 2>&1 | sed -E -e s#\\(/mnt\\)?/\\([a-zA-Z]\\)/#\\\\\\2:/#g"
    ],
```
{% endhint %}

{% hint style="warning" %}
If the build does not work, **check the error messages first**; it is often easy to identify the cause of an error from a message on a line containing the string error.。

To be sure, clean (remove intermediate files in the `objs_???` directory) and rerun the build to be sure. (All operations, including `make clean`, will fail if there are intermediate files left over from builds in other environments).
{% endhint %}



## About WSL

WSL ([Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/about)) is a Linux environment that runs as a subsystem of Windows 10.

{% hint style="warning" %}
On Windows 10, WSL (Windows Subsystem for Linux) is not required to build acts with MWSDK unless there is a specific reason to do so; only those who are already familiar with WSL and want to use it specifically should read this section. This section does not cover how to install or use WSL.
{% endhint %}

### MWSDK2020\_05 .. 2020\_10

You will find both Windows 10 and Linux executables under `MWSDK/Tools/ba-elf-ba2-r36379.w10`, run WSL and set the environment variable `MWSDK_ROOT` appropriately.

For example, for `C:\Work\MWSTAGE\MWSDK`, set the following:

```
$ export MWSDK_ROOT=/mnt/c/Work/MWSTAGE/MWSDK
```

### MWSDK2020\_12

The TWELITE STAGE SDK package does not include an executable for WSL.

Store the complete set of tools in a folder named `MWSTAGE/Tools/ba-elf-ba2-r36379.wsl`. It is easier to use `MWSDK/Tools/ba-elf-ba2-r36379.w10` in MWSDK2020\_10.

### Select a toolツールの選択

`MWSDK/Tools/MkFiles/rules.mk` is used to determine the environment and to select the tools directory. The following is an excerpt of `rules.mk`, which judges the presence or absence of the `WSLENV` environment variable.

```
# Configure for WSL (Windows Subsystem Linux)
ifneq ($(origin WSLENV),undefined)
$(info !!!WSL environment, use Linux toolchain instead.)
TOOLCHAIN_PATH = ba-elf-ba2-r36379.wsl
endif
```

