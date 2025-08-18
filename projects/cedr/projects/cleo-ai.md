---
layout: cedr_layout
title: CLEO-AI
---

# CLEO-AI: Closed-loop Edge System for Optimized and Adaptive Intelligence

CLEO-AI (Closed-loop Edge system for Optimized and Adaptive Intelligence), a novel software-hardware co-design framework for mission-adaptive intelligence in complex, dynamic, and resource-constrained edge systems.

<img src="/projects/cedr/images/cleo-ai-high-level.svg" alt="CLEO-AI" style="display: block; margin: 0 auto;">

## Detailed Overview

Unlike traditional pipelines that separate training, deployment, and adaptation phases, CLEO-AI integrates online model growth, compression, deployment, and runtime management directly on the edge device enabling continuous adaptation with minimal overhead. This makes CLEO-AI a strategic enabler for real-world applications where AI must adapt on the fly to new data, sensor noise, or changing operational contexts. We implement CLEO-AI as a closed-loop framework that includes:

 * Online and on-chip learning to support real-time adaptation
 * Hardware-agnostic deployment across heterogeneous edge processors
 * Runtime management and adaptation of models in response to sensing conditions

CLEO-AI integrates Adaptive Learning System (ALS) with a Runtime System to enable end-to-end model generation, deployment and continuous adaptation while leveraging SoC with heterogeneous processing elements. ALS integrates both model growth and compression in a feedback-driven loop, optimized for edge environments. 