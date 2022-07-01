---
title: "tweterm.py"
author: "Mono Wireless Inc."
description: "tweterm.py"
---
# tweterm.py

This program incorporates the pyftdi (https://github.com/eblot/pyftdi) library sample script pyterm.py with a firmware write script for TWELITE. It has the following features:

* Writing firmware for TWELITE (TWELITE R/MONOSTICK)
* Checking the behaviour of the serial port

{% hint style="warning" %}
This script requires the Python3 interpreter to run on OS X. It is intended for users who are familiar with the command line environment and the Python interpreter.
{% endhint %}

{% hint style="warning" %}
In order to make this script work on Linux, you will need the equivalent packages (libusb-dev, pyserial, pyftdi). It is intended for people who are familiar with the command line environment and the Python interpreter.

* Reference environment: Ubuntu 18.04 (x86-64 64bit), Python 3.6.5&#x20;
{% endhint %}



## System requirements and required packages

* Mac OS X or Linux
* python3.5 or later
* libusb
* pyserial
* pyftdi

### Development environment

We have developed and tested the software in the following environments. However, we do not guarantee that it will work in these environments.

| the environment                         |
| --------------------------------------- |
| Mac OS X 10.11.6, Python3.5.1 (2018/05) |
| Ubuntu 18.04, Python3.6.7 (2018/05)     |
| Mac OS X 10.14.2, Python3.7.2 (2019/01) |



## Installation

### Installing the package

{% hint style="warning" %}
The following procedure may not be directly applicable due to version upgrades or specification changes of the package management system. Please refer to the general information.
{% endhint %}

{% tabs %}
{% tab title="OS X" %}
Below is an example of installing all new packages using Homebrew.

#### Homebrew

Install Homebrew.

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

#### &#x20; Python3

```bash
$ brew install python3
```

#### &#x20;libusb

```bash
$ brew install libusb
```

#### pyserial

```bash
$ pip3 install pyserial
```

#### pyftdi

```bash
$ pip3 install pyftdi
```
{% endtab %}

{% tab title="Linux" %}
Please check your distribution's package installation instructions. You will need the following packages

* python3.5 or later (in most cases it is installed)
* libusb-dev
* pyserial
* pyftdi

Example of package installation commands.

```bash
$ sudo apt-get install libusb-dev
$ sudo apt-get install python3-pip
$ pip3 install pyserial
$ pip3 install pyftdi
```
{% endtab %}
{% endtabs %}

### Execution

The directory where you installed the TWELITE SDK is written as `${TWELITESDK}`.

The script can be found below.

```bash
${TWELITESDK}/Tools/tweterm/tweterm.py
```

Gives the script permission to run.

```bash
$ chmod +x ${TWELITESDK}/Tools/tweterm/tweterm.py
```

Add it to the `PATH` environment variable if necessary.

```bash
$ PATH=${TWELITESDK}/Tools/tweterm:$PATH
```

## Usage

### Unloading the USB driver

{% hint style="warning" %}
Unload (disable) the driver as it conflicts with the OS driver for libusb.
{% endhint %}

{% tabs %}
{% tab title="OS X" %}
Unloads FTDI-related drivers.

```bash
$ sudo kextunload -b com.apple.driver.AppleUSBFTDI
```
{% endtab %}

{% tab title="Linux" %}
There is no need to unload the driver.

{% hint style="warning" %}
If you get an error, try unloading the driver.

```bash
$ sudo rmmod ftdi_sio
$ sudo rmmod usbserial
```
{% endhint %}
{% endtab %}
{% endtabs %}

### &#x20; Command parameters

| Parameters                | Remark                                                      |
| ------------------------- | ----------------------------------------------------------- |
| `-p ftdi:///?`   or `-p`  | Displays a list of devices.                                 |
| `-p [Device name]`        | Specify the device.                                         |
|                           | `ftdi:///1`  When no other device is available.             |
|                           | `ftdi://::MW19ZZUB/1` Designation by serial number.         |
| `-b [baud rate]`          | Specifies the baud rate.                                    |
|                           | `-b 115200`  115200bps is specified.                        |
| `-F [firmware]`           | Write the firmware.                                         |
|                           | `-F App_Twelite.bin` Write a file named App\_Twelite.bin.   |
| `--no-color`              | Suppresses colour output of text.                           |
| `--no-term`               | It only writes the firmware and does not open the terminal. |

### Keyboard operation

Entering the `Ctrl+C` key will bring up a control prompt that allows you to perform some special operations. Otherwise, the input string will be sent directly to the TWELITE radio module.

| Input keys                        | Remarks                                                                                                                                                          |
| --------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Ctrl+C Ctrl+C`                   | Exit the terminal.                                                                                                                                               |
| `Ctrl+C Ctrl+R` または `Ctrl+C r`    | TWELITE Resets the wireless microcontroller.                                                                                                                     |
| `Ctrl+C Ctrl+I` または `Ctrl+C i`    | Enter the + + + command to enter interactive mode. Only available with firmware that supports interactive mode.                                                  |
| `Ctrl+C A`                        | Start interpreting the format: for the output from the TWELITE wireless microcontroller and for the key input, the ascii format is interpreted.                  |
| `Ctrl+C B`                        | Starts interpreting the format; binary format is interpreted for the output from the TWELITE wireless microcontroller. Key input is interpreted in ASCII format. |
| `Ctrl+C N`                        | Stops the interpretation of the format.                                                                                                                          |

{% hint style="info" %}
During format interpretation, only messages from TWELITE that have been interpreted will be displayed, and keyboard input will be echoed back, but will be sent to TWELITE when the ASCII format has been completed.
{% endhint %}

## \[Running example]

In the example, line breaks are inserted as appropriate.

{% hint style="warning" %}
If you get an error, it may be a problem with the permissions on the serial port, run it with root privileges (e.g. sudo).
{% endhint %}

#### ＜Make sure the device is listed first＞

```bash
$ tweterm.py -p ftdi:///?
Available interfaces:
  ftdi://ftdi:232:MW19ZZUB/1   (MONOSTICK)
  Please specify the USB device
```

#### ＜Write the firmware and start the terminal＞

The following example writes App\_UART (UART communication app) and checks the boot message.

```bash
$ tweterm.py -p ftdi://ftdi:232:MW19ZZUB/1 -b 115200 -F ../App_Uart_Master_RED_L1101_V1-2-15.bin 
*** TWE Wrting firmware ... ../App_Uart_Master_RED_L1101_V1-2-15.bin
MODEL: TWEModel.TWELite
SER: 102eebd

 file info: 0f 03 000b
erasing sect #0..#1..#2..
0%..10%..20%..30%..40%..50%..60%..70%..80%..90%..done - 10.24 kb/s
Entering minicom mode

!INF TWE UART APP V1-02-15, SID=0x8102EEBD, LID=0x78
8102EEBD:0> 
```



#### ＜Typing Ctrl+C will bring up a control prompt＞

```
*** r:reset i:+++ A:ASCFMT B:BINFMT x:exit>
```



#### ＜Continue typing i. You are now in interactive mode＞

```
*** r:reset i:+++ A:ASCFMT B:BINFMT x:exit>[+ + +]
--- CONFIG/TWE UART APP V1-02-15/SID=0x8102eebd/LID=0x00 -E ---
 a: set Application ID (0x67720103) 
 i: set Device ID (121=0x79) 
... 
```

If you type + + + three times as usual, you will get the same result.&#x20;



#### ＜Example of format interpretation: Set App\_UART to binary format＞

In interactive mode, type `m` `B` `Enter` `S` in that order.

```
--- CONFIG/TWE UART APP V1-02-15/SID=0x8102eebd/LID=0x00 -E ---
 a: set Application ID (0x67720103) 
 i: set Device ID (121=0x79) 
 c: set Channels (18) 
 x: set RF Conf (3) 
 r: set Role (0x0) 
 l: set Layer (0x1) 
 b: set UART baud (38400) 
 B: set UART option (8N1) 
 m: set UART mode (B)*
 h: set handle name [sadkasldja] 
 C: set crypt mode (0) 
 o: set option bits (0x00000000) 
---
 S: save Configuration
 R: reset to Defaults
 
!INF Write config Success
!INF RESET SYSTEM...
```



#### ＜Examples of format interpretation＞

In the following example, App\_UART does input and output in binary format. Input `Ctrl+C` `B`.

```
*** r:reset i:+++ A:ASCFMT B:BINFMT x:exit>
[FMT: console ASCII, serial BINARY]
```

In this state, input and output is in format. Keyboard input is interpreted as ASCII and messages from TWELITE are interpreted as binary.



Here is an example of receiving a telegram from TWELITE. The easiest way to do this is to reset the TWELITE. Type `Ctrl+C` `r`.

```
*** r:reset i:+++ A:ASCFMT B:BINFMT x:exit>[RESET TWE]
[dbf1677201030001020f008102eebd0000]
```

The output `[dbf...]` is the message from TWELITE, which is actually a binary sequence of `0xdb 0xf1 0x67...`.



Conversely, to send a telegram to TWELITE, enter it in ASCII format. Type `:7800112233AABBCCDDX`. This sends the data with payload `0x7800112233AABBCCDD` to TWELITE in binary format. Immediately afterwards, `[dba18001]` is returned as the response.

```
:7800112233AABBCCDDX[dba18001]
```



#### ＜Exits＞

Type `Ctrl+C` `Ctrl+C`.

```
*** r:reset i:+++ A:ASCFMT B:BINFMT x:exit>[
[EXIT]
Bye
```
