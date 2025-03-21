---
title: Performance
classes: single
permalink: "/docs/benchmarks/"
toc: true
toc_sticky: true
---

### Synthetic benchmarks

Synthetic benchmarks have significant limitations. They fail to represent real-world scenarios and only perform a narrow range of computations, highlighting a small portion of overall performance. Moreover, they are susceptible to manipulation, as one could optimize a CPU implementation or emulation specifically to excel in the benchmark.

Synthetic benchmarks should not be trusted as a reliable performance measure. They are included here merely because many people enjoy making comparisons. However, further down this page, you will find measurements from real-world scenarios, such as archive compression and decompression, music encoding, and 3D scene rendering. More benchmarks will be added over time.

#### AIBB

AIBB is one of the most comprehensive benchmark suites from earlier times, predating tools like SysSpeed and others. The benchmark results are categorized into three groups: integer benchmarks (which include memory speed tests), FPU benchmarks (focused on floating point math computations), and graphics benchmarks.

{% include figure popup=true image_path="/assets/images/AIBB_Integer.png" alt="AIBB integer benchmarks" %}

Please note that the Y-axis is logarithmic to accommodate the wide range of system speeds. This approach is also applied to the FPU benchmarks shown below. The differences in speed between the systems are too vast to be displayed on a linear scale.

{% include figure popup=true image_path="/assets/images/AIBB_FPU.png" alt="AIBB FPU benchmarks" %}

The graphics benchmarks require a brief explanation. They are relatively well-balanced across all systems because they use a bitplane screen mode of the original OCS/AGA chipset. In this setup, the performance is limited by both the chipset and the PiStorm interface to the Amiga.

{% include figure popup=true image_path="/assets/images/AIBB_Gfx.png" alt="AIBB graphics benchmarks" %}

#### SysInfo 4.4

The SysInfo speed test is one of the least reliable for the Amiga. The speed test loop has changed slightly between different SysInfo versions, but the changes in chip memory speed measurement have been significant. If you wish to compare results between different systems, ensure that all tests are conducted using the same version of SysInfo.

Additionally, please note that the Dhrystone result in SysInfo is not an actual Dhrystone benchmark. It is simply the computed MIPS value scaled by a fixed factor.

... plot will follow...

#### CoreMark 1.0

CoreMark ([coremark.org](https://www.eembc.org/coremark/)) is a benchmarking tool developed by the Embedded Microprocessor Benchmark Consortium (EEMBC). It provides a standardized, industry-accepted method for evaluating processor performance across various architectures and implementations. CoreMark includes a range of workloads, such as:
- List processing (find and sort operations)
- Matrix manipulation (common in many algorithms)
- State machine processing (useful for many control-oriented tasks)
- Cyclic redundancy check (CRC) (common in data integrity checking)

The executable is easily portable across different systems. You can find a binary compiled for AmigaOS (68020, no FPU required) [here](/assets/files/coremark_softfloat.zip).

{% include figure popup=true image_path="/assets/images/CoreMark.png" alt="CoreMark 1.0 scores" %}

### Real-world benchmarks
TBD...

#### Doom Attack

The DoomAttack archive is available for download on this website ([link](/assets/files/DoomAttack_Doom1_SW.zip)). After downloading and unpacking the archive, start the demo using the following command:
```
doomattack -forcedemo -timedemo demo3
```
For consistency, use "NTSC: Low res" mode for AGA testing and "320x200x8" mode for RTG tests. The game will start in benchmark mode and conclude with an error message similar to:``Error: timed 2134 gametics in XXXX realtics``. You can calculate the FPS using the following formula:
```
FPS = 35 * (2134 / realticks)
```
Below are the benchmark results for PiStorm and a regular Amiga.

{% include figure popup=true image_path="/assets/images/DOOM_Attack_AGA.png" alt="DOOM Attack, AGA mode" %}
{% include figure popup=true image_path="/assets/images/DOOM_Attack_RTG.png" alt="DOOM Attack, RTG mode" %}

#### LightWave

In this test, you start LightWave 3.5, preferably the FPU version, and load a [scene](http://zgodzinski.com/lightwave_benchmark/lw_35_benchmark.zip) prepared by Piotr Zgodzinski (AKA Jubi). Without making any changes in LightWave, begin the rendering process. The total rendering times for various CPU versions with FPU are provided below. Lower values indicate better performance. 

{% include figure popup=true image_path="/assets/images/LightWave.png" alt="LightWave rendering time" %}

#### MP3 encoding
TBD...
