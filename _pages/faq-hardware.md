---
title: Frequently Asked Questions - Hardware
classes: single
permalink: "/faq/hardware/"
toc: true
toc_sticky: true
---

### Can I use a GPIO extension cable to put the Raspberry Pi outside of the Amiga?

No, this is not going to work. The GPIO is used to communicate with the FPGA/CPLD of PiStorm at
very high speeds (actually almost as fast as GPIO can operate) and thus is very sensitive to any noise. The noise
in this case can be caused by crosstalk between the GPIO wires on the extension cable or signal reflections. 
Simply put, it is not going to work.

### Can I use a microSD extender cable?

That's complicated. The simple answer is you shouldn't. The reason is the same as in the case of [GPIO extenders](#can-i-use-gpio-extension-cable-to-put-raspberry-outside-of-amiga) - high speed sharp-edged signals guided together over long distances, together with a clock line transmitting at 50MHz and its harmonics. If you are 
lucky it will work, but in most cases expect higher number of read/write errors and possibly other unusual behaviour. 
What can  help is reducing the microSD clock rate (the lower the better), at the expense of degraded performance. The best solution 
is not use microSD extenders at all and use other ways to transfer files (e.g. Wi-Fi or CompactFlash via the PCMCIA slot for the A600 and A1200).

### Can I connect extra power supply to the RaspberryPi?

No! Absolutely not! The 5V rail of the Raspberry Pi is already powered from your Amiga. If you connect an external power
supply as well, you will surge power to the Amiga from this supply too. The results will be bad - possibly very bad! If you really feel
the Raspberry Pi needs extra power, then either use a dedicated connector (for example the PiStorm for Amiga 600 has such a connector) or micro USB, but
either way, take the 5V rail from the Amiga, not from any external source.

### But I saw someone powering whole Amiga through a Raspberry Pi...

This is absolutely unsupported and you SHOULD NOT do that! Backpowering the whole Amiga from the Raspberry Pi will not only
put a higher load on the 5V rail of both the Raspberry Pi and the PiStorm, it will also only provide 5V to your Amiga. 
Other required voltages, namely the +12V and -12V will be missing. This means the audio will be horrible, the floppy drive will eventually not be working, the serial port
definitely will not work and many other fancy effects are possible. Just DO NOT DO THAT!

### What about RaspberryPi 5?

Short answer: forget it.

Long answer: Unfortunately, the Raspberry Pi Foundation introduced a south-bridge in the Pi5, an additional chip that handles the GPIO, which is crucial for PiStorm's fast communication between hardware and software. This south-bridge connects to the ARM CPU via a PCIe x4 bus. While the bus itself is excellent for bulk transfers, it has very high setup times, making the GPIO too slow for PiStorm's needs. We are not the only project affected by this limitation, and the Raspberry Pi Foundation is aware of the issue. As a result, we are currently limited to using the Pi Zero 2 W, Pi 3, Pi 4, and CM4.

### Will you be able to use CM5 maybe?

It is highly likely that the CM5 (Compute Module 5) will suffer from the same issue with the GPIO south bridge as the Pi5 (see previous FAQ entry). Therefore, we do not plan to support the CM5 in the future. If a version without the south bridge becomes available, we may reconsider. However, for now the CM5 is not an option for us.
