---
title: Benchmarks
classes: single
permalink: "/docs/benchmarks/"
toc: true
toc_sticky: true
---

# Synthetic benchmarks

Synthetic benchmarks are bad, very bad. They do not show any real world situation and perform only small
subset of different computations to show/test only a bit tiny of the whole. Furthermore, they are prone to
manipulations since one could fine tune given CPU implementation or emulation to match the needs of the benchmark
alone.

Never trust synthetic benchmarks. They are added here just because everyone likes to compare one thing against
the other. Down this page you will also find some measurements from real world scenarios, such as archive compression
or decompression, encoding music, rendering 3d scenes and such. The benchmarks will be added with time.

## AIBB

AIBB is the most comprehensive benchmark suite from the old days, before tools like SysSpeed and others appeared
on the horizon. The benchmark results are divided into three groups - integer benchmarks together with memory speed
test, FPU benchmarks doing a lot of floating point math computations and graphics benchmarks.

{% include figure popup=true image_path="/assets/images/AIBB_Integer.png" alt="AIBB integer benchmarks" %}

Please note that the Y-axis is logarithmic, so that all systems can fit there somehow. The same rule applies to the
FPU benchmarks. There are simply too large differences in speed across the systems to put them on the same scale in
other way.

{% include figure popup=true image_path="/assets/images/AIBB_FPU.png" alt="AIBB FPU benchmarks" %}

The graphics benchmarks require short explanation - they are pretty well balanced across all systems. This is because
they are done on a bitplane screen mode using original OCS/AGA chipset. There, the chipset as well as PiStorm interface
to Amiga are physical limit.

{% include figure popup=true image_path="/assets/images/AIBB_Gfx.png" alt="AIBB graphics benchmarks" %}

## SysInfo 4.4

SysInfo speed test is one of the words in case of Amiga. The speed test loop changed from SysInfo version to version a
little, the change in chip mem speed was however massive. If you would like to compare results between different
systems, please do make sure all tests are done using the very same version of SysInfo software.

Please also note that the Dhrystone result of SysInfo is not a real Dhrystone benchmarks. It is just the computed MIPS
value scaled by a fixed factor.

... plot will follow...

# Real-world benchmarks
TBD...
## LightWave
TBD...
## MP3 encoding
TBD...