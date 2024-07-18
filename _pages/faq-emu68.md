---
title: Frequently Asked Questions - Emu68
classes: single
permalink: "/faq/emu68/"
toc: true
toc_sticky: true
---

### I have found a bug, what now?

Oh, sorry to hear! If the bug you have found is related to Emu68 (CPU, performance etc.), feel free to report it
on Emu68's GitHub page in [Issues](https://github.com/michalsc/Emu68/issues) section. Is the problem related to software running
on AmigaOS side (Emu68 drivers, tools and utilities) then please report it in [Issues](https://github.com/michalsc/Emu68-tools/issues) sectin of Emu68-tools.

Before commiting a report, have a look at other open issues. If you find your issue there, feel free to comment and
vote. If you are sure the issue is new, create a new entry. Please include all information you can think of (PiStorm hardware
version, Emu68 version, Amiga model) and steps necessary to reproduce the issue. A simple "does not work" is usually not enough.

### My A1200 is showing 512kb Chip RAM with PiStorm32, what gives?

Your cmdline.txt has one or more of the ``move_slow_to_chip`` ``enable_c0_slow`` ``enable_c8_slow`` ``enable_d0_slow``  commands in. Remove it/them. They're for machines with less than 2meg Chip.

### Should I install 68040.library?

No, Emu68 provides its own version of ``68040.library`` which is built in into the driver pack ROM. It is autimatically initialized on boot, so a version stored on the hard drive would not even load.

### Should I shutdown Pi when powering Amiga off?

No. Emu68 is bare metal software and has no underlying opeating system requiring a shutdown. When you want to power your Amiga
off, do it just like you always did: watch the activity of all drives and, when they are not in use, switch your Amiga off.

### I've got a working hdf, how do I put that onto an SD for PiStorm?

First, the hdf must be RDB type. Open it in a hex editor and check the first few bytes - if it's RDSK you're good, if it's DOS it won't work - that's not bootable on a real Amiga, only in an emulator. Now head over to [hdf2emu68 tool](https://github.com/PiStorm/hdf2emu68) and follow the instructions there, that tool does all the partitioning needed to make a PiStorm SD and writes your hdf to the ``0x76`` partition.

Finally add the emu68 files to the fat32 partition on the SD and configure it up as normal. 
