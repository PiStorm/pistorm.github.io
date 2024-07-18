---
title: Frequently Asked Questions - Hardware
classes: single
permalink: "/faq/hardware/"
toc: false
---

- [Can I use GPIO extension cable to put Raspberry outside of Amiga?](#can-i-use-gpio-extension-cable-to-put-raspberry-outside-of-amiga)
- [Can I use microSD extender cable?](#can-i-use-microsd-extender-cable)
- [Can I connect extra power supply to RaspberryPi?](#can-i-connect-extra-power-supply-to-raspberrypi)
- [But I saw someone powering whole Amiga through Rasbperry...](#but-i-saw-someone-powering-whole-amiga-through-rasbperry)

## Can I use GPIO extension cable to put Raspberry outside of Amiga?

No, since this is not going to work. The GPIO is used to communicate with the FPGA/CPLD of PiStorm at
very high speeds (actually almost as fast as GPIO can) and thus are very sensitive to any noise. The noise
in this case can be caused by crosstalk between GPIO wires on the extension cable or signal reflections. 
It is not going to work.

## Can I use microSD extender cable?

That's complicated. Simple answer is - you shouldn't. The reason is the same as in case of [GPIO extenders](#can-i-use-gpio-extension-cable-to-put-raspberry-outside-of-amiga) - high speed sharp-edged signals guided 
together over long distances, together with a clock line transmitting at 50MHz and its harmonics. If you are 
lucky - it will work, but in most cases expect higher number of read/write errors. What can eventually help is 
reducing the microSD clock rate, the lower the better, at the expense of degraded performance. Best solution 
would be to not use microSD extenders at all and use other ways to exchange the data (e.g. Wi-Fi or CompactFlash
over PCMCIA slot).

## Can I connect extra power supply to RaspberryPi?

No! Absolutely no! The 5V rail of Raspberry is powered from your Amiga already. If you connect external power
supply there, you will surge power to Amiga from this suppy too. The results will be bad or even worse. If you really feel
the Raspberry needs extra power, use either dedicated connector (for example on PiStorm for Amiga 600) or micro USB, but
in any way, take the 5V fail from Amiga, not from any external source.

## But I saw someone powering whole Amiga through Rasbperry...

This is absolutely unsupported and you SHALL NOT do that! Backpowering whole Amiga from Raspberry will not only
put the 5V rail of Raspberry and of PiStorm on higher load. It will also provide only 5V to your Amiga. Other voltages,
namely +12V and -12V will be missing. It means, the audio will be horrible, floppy drive eventually not working, serial port
definitely not working and many other fancy effects. Just DO NOT DO THAT.