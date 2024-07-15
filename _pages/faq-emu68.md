---
title: Frequently Asked Questions - Emu68
classes: single
permalink: "/faq/emu68/"
toc: true
---

- `My A1200 is showing 512kb Chip RAM with PiStorm32, what gives?`
  Your cmdline.txt has one or more of the ``move_slow_to_chip`` ``enable_c0_slow`` ``enable_c8_slow`` ``enable_d0_slow``  commands in. Remove it/them. They're for machines with less than 2meg Chip.
