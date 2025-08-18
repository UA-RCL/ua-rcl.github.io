---
layout: cedr_layout
title: HOPPERFISH
---

# HOPPERFISH: <u>Ho</u>listic <u>P</u>rofiling with <u>P</u>ortable <u>E</u>xtensible and <u>R</u>obust <u>F</u>ramework <u>I</u>ntended for <u>S</u>ystems with <u>H</u>eterogeneity

HOPPERFISH (<u>Ho</u>listic <u>P</u>rofiling with <u>P</u>ortable <u>E</u>xtensible and <u>R</u>obust <u>F</u>ramework <u>I</u>ntended for <u>S</u>ystems with <u>H</u>eterogeneity), a holistic profiling framework that unifies analysis across the application, runtime, microarchitecture, and hardware layers to streamline robust feature correlation in heterogeneous computing systems.

<img src="/projects/cedr/images/AnomalDetection-workflow.svg" alt="HOPPERFISH Workflow" style="display: block; margin: 0 auto;">

## Detailed Overview

HOPPERFISH is an open-source cross-layer profiling framework for heterogeneous SoCs, enabling synchronized monitoring across applications, runtime, microarchitecture, and hardware. It delivers lightweight, accurate, and portable profiling for real-time anomaly detection and machine learning applications. Equipped with capabilities for real-time monitoring and cross-layer analysis, HOPPERFISH offers:

 * Cross-layer profiling integrated into CEDR runtime, unifying application, runtime, hardware, and microarchitecture features.
 * Thread-safe, timer-triggered sampling for online monitoring without halting execution.
 * Portable feature collection pipeline across CPUs, GPUs, and FPGAs.
 * Modular and extensible design supporting platform-specific events while staying hardware-agnostic.
 * Runtime instrumentation to expose task queues, PE utilization, and low-overhead sampling not available in vendor profilers.

