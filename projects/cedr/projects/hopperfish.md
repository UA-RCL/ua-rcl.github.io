---
layout: cedr_layout
title: HOPPERFISH
---

# Anomaly Detection on Heterogeneous SoC

Distinguishing between normal and abnormal application behavior poses a greater challenge in heterogeneous computing systems compared to homogeneous systems due to varying execution characteristics influenced by factors like differences in programming models, diversity of Processing Elements (PEs), and dynamically changing resource allocation decisions. We develop a profiling framework integrated with an open-source runtime to understand the non-linear correlations among the aforementioned factors. Using this framework as a foundation, we construct an autoencoder model that provides a holistic system view and achieves up to 19% and 13% improvement in abnormal behavior detection accuracy compared to conventional methods such as the One-Class Support Vector Machine and Isolation Forest respectively. We demonstrate the robustness of our approach by executing real-world applications covering radar, communications, and autonomous vehicles domains along with anomalous application scenarios that manipulate behavior or the state of the runtime manager, scheduler, and PEs across three commercial off-the-shelf platforms and three scheduling heuristic policies.
