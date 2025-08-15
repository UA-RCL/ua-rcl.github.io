---
layout: cedr_layout
title: RISC-V
---

# RISC-V based Heterogeneous SoC Emulation Platform

Heterogeneous System-on-Chip (SoC) architectures are becoming attractive for deployment in HPC environments as they deliver performance with energy efficiency and scalability benefits. Particularly the RISC-V is an attractive solution for building heterogeneous systems at HPC scale since it offers ability to customize CPU cores and modularity to integrate with other compute units towards meeting the demands of wide range of computational workloads. Consequently, there is a need for a software ecosystem that facilitates productive application development and deployment on such heterogeneous SoCs, while utilizing system resources effectively. We present a preliminary study over a runtime environment that allows execution of applications written in C/C++ on heterogeneous SoC architectures composed of multiple RISC-V core types and a pool of accelerators emulated on Xilinx Virtex 7 FPGA.  We showcase ability to investigate the impact of hardware composition and scheduling policy on execution time performance while executing real-life applications in our emulation environment.