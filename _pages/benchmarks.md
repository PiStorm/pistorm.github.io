---
title: Benchmarks
classes: single
permalink: "/docs/benchmarks/"
toc: true
toc_sticky: true
---

# Synthetic benchmarks

Synthetic benchmarks have significant limitations. They fail to represent real-world scenarios and only perform a narrow range of computations, highlighting a small portion of overall performance. Moreover, they are susceptible to manipulation, as one could optimize a CPU implementation or emulation specifically to excel in the benchmark.

Synthetic benchmarks should not be trusted as a reliable performance measure. They are included here merely because many people enjoy making comparisons. However, further down this page, you will find measurements from real-world scenarios, such as archive compression and decompression, music encoding, and 3D scene rendering. More benchmarks will be added over time.

## AIBB

AIBB is one of the most comprehensive benchmark suites from earlier times, predating tools like SysSpeed and others. The benchmark results are categorized into three groups: integer benchmarks (which include memory speed tests), FPU benchmarks (focused on floating point math computations), and graphics benchmarks.

{% include figure popup=true image_path="/assets/images/AIBB_Integer.png" alt="AIBB integer benchmarks" %}

Please note that the Y-axis is logarithmic to accommodate the wide range of system speeds. This approach is also applied to the FPU benchmarks shown below. The differences in speed between the systems are too vast to be displayed on a linear scale.

{% include figure popup=true image_path="/assets/images/AIBB_FPU.png" alt="AIBB FPU benchmarks" %}

The graphics benchmarks require a brief explanation. They are relatively well-balanced across all systems because they use a bitplane screen mode of the original OCS/AGA chipset. In this setup, the performance is limited by both the chipset and the PiStorm interface to the Amiga.

{% include figure popup=true image_path="/assets/images/AIBB_Gfx.png" alt="AIBB graphics benchmarks" %}

## SysInfo 4.4

The SysInfo speed test is one of the least reliable for the Amiga. The speed test loop has changed slightly between different SysInfo versions, but the changes in chip memory speed measurement have been significant. If you wish to compare results between different systems, ensure that all tests are conducted using the same version of SysInfo.

Additionally, please note that the Dhrystone result in SysInfo is not an actual Dhrystone benchmark. It is simply the computed MIPS value scaled by a fixed factor.

... plot will follow...

# Real-world benchmarks
TBD...

## LightWave

In this test, you start LightWave 3.5, preferably the FPU version, and load a [scene](http://zgodzinski.com/lightwave_benchmark/lw_35_benchmark.zip) prepared by Piotr Zgodzinski (AKA Jubi). Without making any changes in LightWave, begin the rendering process. The total rendering times for various CPU versions with FPU (and for the 68020 and 68000 **without** it) are provided below. Lower values indicate better performance. The x-axis of the plot is logarithmic for clarity due to the wide range of rendering times.

{% include figure popup=true image_path="/assets/images/LightWave.png" alt="LightWave rendering time" %}

## MP3 encoding
TBD...