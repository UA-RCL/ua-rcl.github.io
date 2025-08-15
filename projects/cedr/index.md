---
layout: cedr_layout
title: CEDR Overview
---

# CEDR Overview
System designers are continuously exploring design methodologies that harness increased levels of heterogeneity towards pushing the boundaries of achievable performance gains. We have developed CEDR, an open-source, unified compilation, and runtime framework designed for heterogeneous systems, as part of the DARPA DSSoC program. 
<!--
System designers are continuously exploring design methodologies that harness increased levels of heterogeneity towards pushing the boundaries of achievable performance gains. We have developed CEDR, an open-source, unified compilation, and runtime framework designed for heterogeneous systems, as part of the DARPA DSSoC program. CEDR allows applications, scheduling heuristics, and accelerators to be co-designed in a cohesive manner. CEDR is currently being leveraged in basic research as part of the DARPA SpaceBACN and PROWESS programs. Its utility has been successfully tested by our industry partners General Dynamics and Collins Aerospace with their applications along with several academic partners and independently evaluated by the Carnegie Mellon University Software Engineering Institute. We shared CEDR with the community by organizing tutorials in venues such as International Symposium on Field Programmable Gate Arrays (ISFPGA’24) and Embedded Systems Week, Education Track (ESWEEK’23).  We showcased the utility of this framework through live demonstrations during Free and Open-source Software Developers’ European Meeting (FOSDEM’20 and ’21), GNU Radio 4.0 Hackfest (2020), GNU Radio Conference (2022), and Arm Research Summit (2019).
-->
<img src="images/CEDR-Overview.svg" alt="CEDR Flow" style="display: block; margin: 0 auto; ">

## Key Features of CEDR

<ul>
  <li><strong>Scalability:</strong> Manages execution of dynamically arriving workloads with an arbitrary number of interleaved tasks across heterogeneous compute resources.</li>
  <li><strong>Flexibility:</strong> Supports integration of a wide variety of software-based schedulers through plug-and-play interfaces.</li>
  <li><strong>Portability:</strong> Operates across a wide range of Linux-based SoC platforms, including FPGA (Xilinx ZCU102, Virtex UltraScale+ VCU128, VC707, along with Synopsys HAPS100), GPU (NVIDIA Jetson AGX Xavier), ARM (Odroid XU4, OKdo ROCK5B), and RISC-V emulation environments.</li>
  <li><strong>Abstraction:</strong> Provides a hardware-agnostic application programming interface (API) model that enables users to develop, compile, and deploy applications across heterogeneous computing platforms, including CPUs, GPUs, and FPGAs, without requiring platform-specific programming expertise.</li>
  <li><strong>Interoperability:</strong> Integrates seamlessly with other programming models such as Taskflow, GNURadio, and PyTorch.</li>
</ul>

## Overview Paper
{% include list.html data="citations" component="citation" style="rich" filters="overview: true"%}

## Collaborative Partners

<div style="display: flex; gap: 20px; justify-content: center; flex-wrap: wrap;">
  <!-- Academic Partners -->
  <div style="flex: 1 1 300px; border: 1px solid #ddd; border-radius: 8px; padding: 16px; text-align: center; box-shadow: 0 2px 5px rgba(0,0,0,0.1);">
    <h3>Academic Partners</h3>
    <div style="display: flex; justify-content: center; flex-wrap: wrap; gap: 10px; margin-top: 10px;">
      <img src="/projects/cedr/images/logos/university/UA-logo.png" alt="UA" style="height: 125px;">
      <img src="/projects/cedr/images/logos/university/ASU-logo.png" alt="ASU" style="height: 125px;">
      <img src="/projects/cedr/images/logos/university/UM-logo.png" alt="UM" style="height: 125px;">
      <img src="/projects/cedr/images/logos/university/UW-logo.png" alt="UW" style="height: 125px;">
    </div>
  </div>

  <!-- Industrial Partners -->
  <div style="flex: 1 1 300px; border: 1px solid #ddd; border-radius: 8px; padding: 16px; text-align: center; box-shadow: 0 2px 5px rgba(0,0,0,0.1);">
    <h3>Industrial Partners</h3>
    <div style="display: flex; justify-content: center; flex-wrap: wrap; gap: 10px; margin-top: 10px;">
      <img src="/projects/cedr/images/logos/industry/Collins-Aerospace-logo.png" alt="Collins Aerospace" style="height: 125px;">
      <img src="/projects/cedr/images/logos/industry/DASHtech-logo.webp" alt="DASH Tech" style="height: 100px;">
      <img src="/projects/cedr/images/logos/industry/gdms-logo.png" alt="GD" style="height: 40px;">
      <img src="/projects/cedr/images/logos/industry/JHU-APL-logo.webp" alt="APL" style="height: 50px;">
      <img src="/projects/cedr/images/logos/industry/ARM-logo.svg" alt="ARM" style="height: 100px;">
      <img src="/projects/cedr/images/logos/industry/CMU-SEI-logo.jpg" alt="SEI" style="height: 100px;">
    </div>
  </div>
</div>


## Research Initiatives

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 1rem; align-items: center;">
  <img src="/projects/cedr/images/logos/agency/DARPA-logo.png" alt="DARPA" style="width: 100%;">
  <img src="/projects/cedr/images/logos/agency/NSF-logo.png" alt="NSF" style="width: 100%;">
  <img src="/projects/cedr/images/logos/agency/AFRL-logo.png" alt="AFRL" style="width: 100%;">
</div>