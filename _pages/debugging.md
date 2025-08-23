---
title: Debugging
classes: single
permalink: "/docs/debugging/"
toc: true
toc_sticky: true
---

### Foreword

Emu68, the core of the PiStorm accelerator, is a bare-metal software. Because of this, 
it cannot write debug information to the SD card, USB, or network, as all of these 
interfaces are, or will be, controlled by AmigaOS m68k drivers.

If you need to obtain debug data from Emu68, a serial interface must be attached 
to the PiStorm. With the help of a second machine, you can either monitor the live 
debug stream as it is produced or record it for later analysis.

Emu68 supports two modes of operation for the debug interface:

* Asynchronous RS232 unidirectional transmission at 926 kbps (kilobits per second)
* Synchronous unidirectional transmission at variable speeds

In both cases, the data is generated and transmitted using a bit-banging technique. 
This is necessary because none of the available GPIO alternate functions on the 
Raspberry Pi allow the use of a hardware serial port. As a result, asynchronous RS232 
mode may suffer from significant transmission errors, since two CPU cores attempt to 
bit-bang the GPIO lines simultaneously: CPU0 for Emu68–PiStorm communication and CPU1
 for sending debug data from a ring buffer.

For this reason, the synchronous mode is recommended. Here, clock information is sent 
over an additional wire, which ensures reliable transmission even when the data rate 
varies due to concurrent GPIO activity. Since no strict timing rules need to be followed, 
this mode is also faster and less intrusive, particularly when large volumes of debug 
data are generated.

### Hardware interface

If you choose the RS232 mode, you are free to use any 3.3 V TTL-compatible serial 
interface. Based on the PiStorm community’s experience, FTDI-based adapters have 
proven to be reliable. The transmission format is 8N1: 8 data bits, no parity, and one 
stop bit, which is a standard configuration for low-level serial debugging.

For synchronous mode, use an interface based on the **FT232H** family of chips. Be sure 
to select an **H** version (FT232H, FT2232H, FT4232H); the regular FT232 will not work 
because it does not support the required fast serial mode. In synchronous mode, two 
signals are used:
* AD0 - data wire
* AD1 - clock wire

These two pins can usually be found on the board of your chosen interface, labeled 
either as D0/D1 or ADBUS0/ADBUS1. Refer to the board documentation or schematic to 
confirm. If in doubt, the
[Adafruit FT232H breakout](https://www.adafruit.com/product/2264) board is a safe option.

Before use, the FT232H interface typically requires one additional step: the fast 
serial mode must be enabled with the [FT_Prog](https://ftdichip.com/utilities/) tool 
from FTDI. In this tool, configure the port connected to the debug interface to 
OPTO Isolate mode, as shown below:

![ft_prog](/assets/images/debugging/ft_prog.png)

After switching to OPTO Isolate mode, your FT232H interface is ready to use.

#### Classic PiStorm

On the classic PiStorm, the serial interface is not explicitly exposed. You will need 
to solder either two or three wires -- GND, Data, and optionally Clock -- to the 40-pin 
Raspberry Pi header. This can be done on either the Raspberry Pi side or the PiStorm 
side. The relevant signals are:

* RS232 mode: data on **GPIO26** (Pin 37)
* Synchronous mode: clock on **GPIO26** (Pin 37), data on **GPIO27** (Pin 13)

Please refer to the official RaspberryPi documentation for location of these GPIO pins on 
the connector.

#### PiStorm32-Lite

On the PiStorm32-Lite, the debug header is available on the extension port:

![ps32lite_debug](/assets/images/debugging/ps32lite_debug.png)

Debug signals:
* Pin 0 (marked with a square) carries the data signal.
* Pin 1 carries the clock signal when using synchronous mode.
* GND is also available on the same connector.

#### PiStorm16

The PiStorm16 uses the same extension port as the PiStorm32-Lite, but it is located on 
the edge of the board. The top side of the connector exposes pins 0, 2, 4, 6, and 8, while
the bottom side carries pins 1, 3, 5, 7, and 9. Pin 0 is marked with a small triangle 
on the top side of the board:

![ps16_debug](/assets/images/debugging/ps16_debug.png)

Debug signals:
* Pin 0 provides the data signal in both modes of operation.
* Pin 1 (on the bottom side) provides the clock signal in synchronous mode.
* GND is available on Pin 8 of this connector

In addition, the same debug signals are exposed on a JST connector labeled **DBG**, with
the following pin order (left to right): GND, Clock, Data.

### Software

#### FastSerial

For receiving debug data in synchronous mode, you can use the FastSerial tool. This is a 
command-line utility based on the FTDI ftd2xx libraries. Please install the drivers from
[this link](https://ftdichip.com/wp-content/uploads/2025/03/CDM-v2.12.36.20-WHQL-Certified.zip).

The FastSerial project will soon be available on GitHub. For now, you can download prebuilt 
executables:

* Windows 11 (x64): [FastSerial_win64.zip](/assets/files/FastSerial_win64.zip) 
* Linux (x86_64): [FastSerial_linux_x64.zip](/assets/files/FastSerial_linux_x64.zip)
A macOS build will be provided later.

Once the FTDI drivers are installed, start the FastSerial executable:

```
> FastSerial.exe
Listening on fast serial port...
```

As soon as Emu68 starts transmitting debug data, it will appear in the console.
To store the debug output while still displaying it, specify a log file name as a parameter:

```
> FastSerial.exe some_log_file.txt
Listening on fast serial port...
```

On Linux, additional setup may be required. The system will often load its own default 
kernel modules, which conflict with ``libftd2xx.so`` when accessing the FT232H chip directly. 
If this happens, you will see the following message:

```
$ ./FastSerial 
FT_Open(0) failed, with error 3.
Use lsmod to check if ftdi_sio (and usbserial) are present.
If so, unload them using rmmod, as they conflict with ftd2xx.
```

In that case, unload the conflicting module with:

```
$ sudo rmmod ftdi_sio
$ ./FastSerial
Listening on fast serial port...
```

To avoid repeating this step after each reboot, consider updating your kernel module 
blacklist to prevent ``ftdi_sio`` from loading automatically. Also, make sure you have 
the correct access rights to the USB device so that you do not need to run ``FastSerial``
with administrator privileges.

#### Watching JIT as it is working

