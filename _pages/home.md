---
permalink: /
author_profile: false
layout: splash
title: "Welcome!"
header:
  image: /assets/images/pistorm_splash.jpg
  caption: "Image credit: [@edu_arana](https://x.com/edu_arana)"
intro:
  - excerpt: >
      PiStorm is a hardware project designed to enhance capabilities of your Amiga 
      significantly. It involves RaspberryPi single board computer which replaces
      the 680x0 series CPU of your machine providing a significant boost in performance.<br/><br/>
      Key features of PiStorm
feature_row:
  - title: "Open Source"
    excerpt: >
      Both PiStorm hardware and software are released under open source licenses ranging from BSD-alike
      to MPLv2. Build PiStorm, buy it, download software from GitHub or sarch for ready to use 
      distributions. It's up to you.
    url: "/docs/license/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Performance"
    excerpt: >
      PiStorm is fast. Very fast. The virtual CPU provided by Emu68 is a bare-metal JIT solution translating m68k
      instruction stream to AArch64. The performance varies depending on the translate code and can go as high as 1MIPS/1MHz.
    url: "/docs/benchmarks/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Compatibility"
    excerpt: >
      While aiming at highest possible performance, it is possible to adjust speed of the virtual CPU according
      to the needs. Change the JIT parameters of Emu68 in real time and watch old CPU sensitive demos like 
      e.g. State-of-the-art, or go for full speed when working with 3D software.
    url: "/docs/compatibility/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
---
{% include feature_row id="intro" type="center" %}
{% include feature_row %}
