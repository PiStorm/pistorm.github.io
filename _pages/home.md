---
permalink: /
author_profile: false
layout: splash
title: "PiStorm - Open Source Accelerator for your Amiga"
header:
  image: /assets/images/pistorm_splash.jpg
  caption: "Image credit: [@edu_arana](https://x.com/edu_arana)"
intro:
  - excerpt: >
      PiStorm is a hardware project designed to enhance capabilities of your Amiga 
      significantly. It involves RaspberryPi single board computer which replaces
      the 680x0 series CPU of your machine providing a significant boost in performance.
feature_row:
  - title: "Open Source"
    excerpt: >
      Both PiStorm hardware and software are released under open-source licenses, ranging from BSD-like to MPLv2. You can build, buy, or sell PiStorm, and download the software from GitHub for free, or look for ready-to-use distributions. The choice is yours. Contributions to the project are also welcome.
    url: "/license/usage/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Performance"
    excerpt: >
      PiStorm is incredibly fast. The virtual CPU provided by Emu68 uses a bare-metal JIT solution to translate the m68k instruction stream to AArch64. Performance varies depending on the translated code, reaching up to 1 MIPS per MHz. For the first time, you can truly enjoy CPU-intensive software.
    url: "/docs/benchmarks/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
  - title: "Compatibility"
    excerpt: >
      While aiming for the highest possible performance, you can adjust the speed of the virtual CPU to suit your needs. Modify the JIT parameters of Emu68 in real-time and enjoy CPU-sensitive demos like "State-of-the-Art," or switch to full speed when working with 3D software.
    url: "/docs/compatibility/"
    btn_class: "btn--primary"
    btn_label: "Learn more"
---
{% include feature_row id="intro" type="center" %}
{% include feature_row %}
