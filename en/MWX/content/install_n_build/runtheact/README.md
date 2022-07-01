---
title: "Executing an ACT"
author: "Mono Wireless Inc."
description: "Executing an ACT"
---
# Executing an ACT

This section describes how to write and execute an ACT (BIN file).

{% hint style="warning" %}
This section is a description of the utility TWE-Programmer in a Windows 10 environment.

On Linux/macOS, [tweterm.py](tweterm.py.md) is used. Please use tweterm.py after referring to the writing and execution flow on this page.
{% endhint %}

{% hint style="info" %}
TWE-Programmer and tweterm.py provide BIN file writing and terminal functions, although terminal software for individual systems can be used for these functions.

* Windows10: TeraTerm
* Linux/macOS: screen, etc...
{% endhint %}



## Writing and executing a BIN file

The resulting BIN file can then be written to TWELITE using TWE-Programmer. See here for more information on how to use it.

{% hint style="danger" %}
Once the BIN file is ready, you can run it on the actual machine. The actual device is a sensitive electronic component, so please handle it with care. The following is a list of typical precautions.

In many cases, especially with the TWELITE R, the electronic board is in direct contact with the outside world without a case, which can lead to unintentional shorts, noise and other problems with the USB device.

In this case, closing the application and unplugging the USB device will usually recover it. In the worst case, the USB device may be damaged or your PC may be damaged.

Take care when handling the electronic circuit boards.

* Wrong circuit
  * Check the circuit **again** before switching it on.
  * Take care against **reverse** **battery insertion** and **over-voltage.**
* Static electricity
  * Even voltages that are not sensed by humans can cause semiconductor failures. It is not necessary to take large measures, but simple measures such as touching metal parts before working, wristbands and special mats can be effective.
* Short circuit due to contact with metal objects
  * Make sure that there are no metal objects near the electronic board. For example, if there are paper clips scattered around, this can cause a short circuit, or a dangerous situation where the battery is heavily discharged and heats up.
{% endhint %}



### 1. Plug the MONOSTICK or TWELITE R into your PC and complete the driver setup beforehand.

Once the device is recognised, a new COM port will be added. If there is more than one COM port and it is difficult to tell, please observe the COM port when it is unplugged and when it is plugged in.

![Example of Device Manager screen](<../../.gitbook/assets/image (10).png>)

{% hint style="warning" %}
If you cannot find the device in the device manager, please try to install the driver from [FTDI](https://ftdichip.com), select the driver for FT232R.
{% endhint %}

### 2. Start TWE-Programmer.exe.

Open the `{MWSDK installation directory}/Tools/TWE-Programmer` directory and double click on TWE-Programmer.exe.

![](<../../.gitbook/assets/image (9).png>)

When TWE-Programmer.exe is started the following screen will appear. In the example screen, a MONOSTICK has been plugged in and assigned to COM6 prior to start up.

![](<../../.gitbook/assets/image (11).png>)

{% hint style="warning" %}
If you do not see MONOSTICK or TWELITE R, please try the following

* Exit the TWE-Programmer.
* Unplug the MONOSTICK or TWELITE R from the PC.
* Plug in the MONOSTICK or TWELITE R again.
* Start TWE-Programmer.

If this doesn't work, you can also try the following:

* Remove as many other USB devices as possible from the PC.
* Reboot the PC and try plugging in the MONOSTICK or TWELITE R.
* Try to re-install the FTDI drivers.
{% endhint %}

### 3. specify the BIN file in the TWE-Programmer.

![](<../../.gitbook/assets/image (12).png>)



Specify the BIN file from the file dialog.

![BIN File Selection](<../../.gitbook/assets/image (26).png>)

### 4. Writing BIN files

Writing a BIN file is automatic when a BIN file is specified.

![BIN file being written](<../../.gitbook/assets/image (15).png>)



### 5-1. On successful write

{% hint style="success" %}
If the write is successful, TWELITE will automatically reset and the terminal will be displayed (if the option to connect to the terminal is checked).

The act file supplied with the MWSDK will display a message on startup. If you see any messages, you can be sure that the write operation has finished successfully and that the act on the TWELITE radio module is running successfully.
{% endhint %}

![After writing (the terminal starts and a start message is displayed)](<../../.gitbook/assets/image (16).png>)

{% hint style="info" %}
If you want to edit the act and write it again while keeping the terminal open, press Ctrl+Alt+W.
{% endhint %}

### 5-2. On write failure

In the event of an unsuccessful write operation, the terminal will not open and the background of the TWE-Programmer window will turn pink.

![Example of screen when writing fails](<../../.gitbook/assets/image (18).png>)

{% hint style="warning" %}
If the write operation fails, press the (re)write button and try again.

If the TWE-Programmer does not respond to your request or if you have any other problems, please follow the instructions below and try again from the USB connection.

* Quit TWE-Programmer.
* Unpluing the MONOSTICK or TWELITE R.
* In some cases you may need to restart your PC.
{% endhint %}

{% hint style="warning" %}
During a write operation with TWELITE PAL, the hardware watchdog timer may be triggered and the write operation may be interrupted. Please retry the write operation.
{% endhint %}
