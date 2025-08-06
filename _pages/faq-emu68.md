---
title: Frequently Asked Questions - Emu68
classes: single
permalink: "/faq/emu68/"
toc: true
toc_sticky: true
---

### I have found a bug, what now?

Oh, sorry to hear that! If the bug you have found is related to Emu68 (CPU, performance etc.), feel free to report it
on Emu68's GitHub page in the  [Issues](https://github.com/michalsc/Emu68/issues) section. If the problem is related to software running
on the AmigaOS side (Emu68 drivers, tools and utilities) then please report it in [Issues](https://github.com/michalsc/Emu68-tools/issues) 
section of Emu68-tools.

Before committing a report, have a look at other open issues. If you find your issue there, feel free to comment and vote on that issue.
If you are sure the issue is new, create a new entry. Please include all information you can think of (PiStorm hardware version, Emu68 version, 
Amiga model, etc.) and any steps necessary in order to reproduce the issue. A simple "it does not work" is usually not enough to diagnose and fix the issue.

### My A1200 is showing 512kb Chip RAM with PiStorm32, what gives?

Your cmdline.txt has one or more of the ``move_slow_to_chip`` ``enable_c0_slow`` ``enable_c8_slow`` ``enable_d0_slow``  commands in. Remove it/them. They're for machines with less than 2meg Chip RAM.

### Should I install the 68040.library?

No, Emu68 provides its own version of ``68040.library`` which is built in to the driver pack ROM. It is automatically initialized on boot, so a version stored on the hard drive would not even load.

### Should I shutdown the Pi when powering Amiga off?

No. Emu68 is bare metal software and has no underlying operating system requiring a shutdown. When you want to power your Amiga
off, do it just like you always did: watch the activity of all drives and, when they are not in use, switch your Amiga off. If using PFS, 
remember that the delayed writes can mean you need to wait a few seconds before doing so to prevent file system corruption!

### I've got a working hdf, how do I put that onto an SD for PiStorm?

First, the hdf must be RDB type. Open it in a hex editor and check the first few bytes - if it's marked as RDSK you're good, if it's DOS it won't work - that's not bootable on a real Amiga either, only in an emulator. Now head over to [hdf2emu68 tool](https://github.com/PiStorm/hdf2emu68) and follow the instructions there, that tool does all the work needed to take your hdf image, create a ``0x76`` partition, and make an image suitable for writing to a microSD card that is suitable for use in your PiStorm.

Once you have written the image to your microSD card (using an imaging tool of your choice), add the Emu68 files to the fat32 partition on the SD and configure it as normal. 

### Can I change the CPU type in Emu68?

No, Emu68 does not emulate any specific CPU type. It identifies itself as a 68040 solely to support a particular set of supervisor instructions for system maintenance. Beyond this, it has no similarities with any member of the 680x0 family. It features distinct instruction execution timings, architecture, caches, and operating principles, none of which can be altered.

### Can I turn off JIT?

Short answer: Yes, by powering off your Amiga.

Longer answer: Emu68 is exclusively a Just-In-Time (JIT) engine. It does not have an interpreter mode that can be enabled upon request. Although an interpreter mode might be developed in the distant future, for now, Emu68 operates solely as a JIT engine. Despite this, Emu68 is highly customizable at runtime, allowing you to enjoy legacy software such as games, demos, and other applications.
