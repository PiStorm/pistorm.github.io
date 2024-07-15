---
title: Frequently Asked Questions - Emu68
classes: single
permalink: "/faq/emu68/"
toc: true
---

- [I have found a bug, what now?](#i-have-found-a-bug-what-now)
- [My A1200 is showing 512kb Chip RAM with PiStorm32, what gives?](#my-a1200-is-showing-512kb-chip-ram-with-pistorm32-what-gives)

## I have found a bug, what now?

Oh, sorry to hear! If the bug you have found is related to Emu68 (CPU, performance etc.), feel free to report it
on Emu68's GitHub page in [Issues](https://github.com/michalsc/Emu68/issues) section. Is the problem related to software running
on AmigaOS side (Emu68 drivers, tools and utilities) then please report it in [Issues](https://github.com/michalsc/Emu68-tools/issues) sectin of Emu68-tools.

Before commiting a report, have a look at other open issues. If you find your issue there, feel free to comment and
vote. If you are sure the issue is new, create a new entry. Please include all information you can think of (PiStorm hardware
version, Emu68 version, Amiga model) and steps necessary to reproduce the issue. A simple "does not work" is usually not enough.

## My A1200 is showing 512kb Chip RAM with PiStorm32, what gives?

Your cmdline.txt has one or more of the ``move_slow_to_chip`` ``enable_c0_slow`` ``enable_c8_slow`` ``enable_d0_slow``  commands in. Remove it/them. They're for machines with less than 2meg Chip.
