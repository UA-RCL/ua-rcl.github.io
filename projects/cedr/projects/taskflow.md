---
layout: cedr_layout
title: Taskflow
---

# A Unified Portable and Programmable Framework for Task-Based Execution and Dynamic Resource Management

Heterogeneous computing systems are essential for addressing the diverse computational needs of modern applications. However, they present a fundamental trade-off between easy programmability and performance. This paper addresses this trade-off by enabling performance and energy efficiency optimization while facilitating easy programming without delving into hardware details. It introduces CEDR-Taskflow, a comprehensive framework that automatically parallelizes user applications and dynamically schedules its tasks to heterogeneous platforms, enabling efficient resource utilization and ease of programming. Emulation-based studies on the Xilinx ZCU102 and NVIDIA Jetson AGX Xavier SoC platforms demonstrate that this integrated framework improves application execution time by up to 1.47x compared to state-of-the-art, while maintaining hardware-agnostic application development. Furthermore, this integration approach enables features such as streaming-enabled execution and schedule caching that reduce the time spent on task scheduling by up to 29.6x and results in up to 6.1x lower execution time.
