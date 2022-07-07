---
title: "Sample ACTs"
author: "Mono Wireless, Inc."
description: Sample Acts
---

# Sample ACTs

To help you understand how the ACT works, we have prepared some samples.

{% hint style="info" %}
The samples can be found in Act\_samples in the folder where you installed the MWSDK.
{% endhint %}

## Introduction to sample ACTs

The following is intended to be viewed in order from top to bottom.

[act0..4](act\_opening.md) is a very simple example, without any radio functions, to give you an idea of the basic structure of Act.

[Scratch](scratch.md) is a simple code that receives 1 byte commands from the UART, sends them and so on.

[Slp\_Wk\_and\_Tx](slp\_wk\_and\_tx.md) uses a state machine and intermittent operation with sleep, repeating the process of sleep recovery, radio transmission and sleep.

[Parent\_MONOSTICK](parent\_monostick.md) exclusively receives and outputs the reception result to the serial port. The wireless packets in this sample, which are addressed to the parent device (0x00) or to the child device broadcast (0xFE), can be received. It also includes a procedure to add the interactive mode [\<STG\_STD>](../settings/stg\_std.md) to Act.

[PingPong](pingpong.md) is a sample of sending packets from one side to the other and receiving packets back by the other side. It contains basic procedures for sending and receiving.

[BRD\_APPTWELITE](brd\_apptwelite.md) provides bidirectional communication using digital input, analogue input, digital output and analogue output. It also contains the procedure for adding the interactive mode [\<STG\_STD>](../settings/stg\_std.md) to Act.

[PAL\_AMB](pal\_amb.md), [PAL\_MOT-single](pal\_mot-oneshot.md) and [PAL\_MAG](pal\_mag.md) are samples for various PAL boards (you can also run PAL\_MOT and PAL\_MAG in TWELITE CUE by modifying the sample definitions). get, send and sleep sensor values on PAL board.

### ACTs advaiced

* [PAL\_AMB\_usenap](pal\_amb-usenap.md) is a sample that aims to save more power by allowing the TWELITE microcontroller to sleep briefly during the sensor's operating time, which can take several tens of milliseconds.
* [PAL\_AMB\_behavior](pal\_amb-behavior.md) is a behavioural example: in PAL\_AMB the temperature and humidity sensors are called by the code inside the library, but this sample also includes its own procedure for accessing the temperature and humidity sensors.
* [PAL\_MOT\_fifo](pal\_mot.md) for continuous acquisition and wireless transmission of samples without interruption, using the accelerometer's FIFO and FIFO interrupts.
* [PulseCounter](pulsecounter.md) uses a pulse counter function to count the number of pulses detected on the input port, even during sleep, and to transmit this data wirelessly.
* [WirelessUART](wirelessuart.md) interprets the UART input into ASCII format using [serparser](../api-reference/classes/ser\_parser.md) and sends it.
* Setting provides a higher degree of customisation of the interactive mode [\<STG\_STD>](../settings/stg\_std.md).



### ACT, which introduced the stand-alone function

Acts with names starting with [Unit](unit\_acts.md) are intended to introduce features and APIs.



## Get the latest version.

{% hint style="info" %}
We have put the complete source on Github for the purpose of checking the latest code and the revision history between MWSDK versions. See the links below for more information.

[https://github.com/monowireless/Act\_samples](https://github.com/monowireless/Act\_samples)
{% endhint %}



## Common description

The following items are common settings in the Act sample and are explained below.

```cpp
const uint32_t APP_ID = 0x1234abcd;
const uint8_t CHANNEL = 13;
const char APP_FOURCHAR[] = "BAT1";
```

{% hint style="info" %}
The following settings are common to all sample acts.

* Application ID `0x1234abcd`
* Channel `13`

Both the application ID and the channel are mechanisms to ensure that the network does not mix with other networks.

Systems with different Application IDs will not mix, even if they are on the same channel. However, if a system with a different Application ID is transmitting frequently, this will cause interference and will have an effect.

The channel determines the frequency used for communication; in principle, 16 channels are available on the TWELITE radio module, and it is not possible to communicate with different channels except in very exceptional cases, which would not be the case in a normal system.

As a common specification of sample acts, the payload (data part) of the packet is prefixed with a 4-byte string (`APP_FOURCHAR[]`). This is for explanatory purposes, although one byte is sufficient for species specific identifiers. The inclusion of such system-specific identifiers and data structures is another way to prevent confusion.
{% endhint %}

