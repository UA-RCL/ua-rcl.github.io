---
title: FPGA'24 Tutorial Introduction
style: /_styles/presentations/fpga24/custom.css
---

# CEDR: A Holistic Software and Hardware Design Environment for FPGA-Integrated Heterogeneous Systems

As the FPGAs are being embedded in all layers of computing infrastructure from edge to HPC scales, system designers continue to explore design methodologies that leverage increased levels of heterogeneity to meet target performance goals or constraints. In line with this, we have developed CEDR, an open-source, unified compilation and runtime framework designed for FPGA-integrated heterogeneous systems. CEDR allows applications, scheduling heuristics, and accelerators to be co-designed in a cohesive manner. This tutorial builds on the educational class conducted on the CEDR framework during ESWEEK’23 with a focus on FPGA-integrated heterogeneous systems. It caters to audiences with diverse backgrounds and varying levels of expertise, providing an opportunity for exploration and study of FPGA-based computing in heterogeneous contexts.

We will start with an overview of CEDR, and then we will explore how CEDR (i) allows naive application developers to utilize FPGA-based acceleration within heterogeneous environments, (ii) enables system designers to sweep hardware compositions and measure their impact on realistic workload scenarios, and (iii) provides a rich environment for resource management developers to design new scheduling policies. Throughout the tutorial, our common goal is lifting the barriers to research and enabling productive application deployment on FPGA-integrated heterogeneous systems.

{%
  include portrait.html
  name="Sahil Hassan"
  description="Sahil Hassan is a Post-Doc in the Reconfigurable Computing Lab graduating in Spring 2024. His research interests include design and development of resource management techniques for emerging heterogeneous embedded computing systems, novel architectures and algorithms for neuromorphic computing, and FPGA based reconfigurable architectures."
  image="/images/profiles/lab/sahil_hassan.jpg"
  custom-class="wide-profile"
%}

{% 
  include portrait.html
  name="Serhan Gener"
  description="Serhan Gener is a senior PhD student in the Reconfigurable Computing Lab graduating in Spring 2025. His research interests include reconfigurable computing, embedded systems heterogeneous computing, and software security."
  image="/images/profiles/lab/serhan_gener.jpg"
  custom-class="wide-profile"
%}

## Schedule:

- Downloading and building CEDR (5 min)  
- CEDR Overview and capabilities (15 min) 
- Hands-on Exercise 1 (60 minutes) 
  - Deploying reference applications on systems composed of ARM CPUs and FPGA accelerators.  
    - Activity: Prepare reference C/C++ Radar Correlator implementation by introducing CEDR API calls to the application, walk through the compilation flow and deploy on the ZCU102 platform. 
- Hands on exercise 2: (30 minutes)
  - Design space exploration on systems composed of ARM CPUs and FPGA accelerators.  
    - Activity: Vary number of compute resources across different scheduling heuristics (round robin, minimum execution time, earlies finish time) in dynamically arriving workload scenarios. Radar correlator and Pulse Doppler applications will be launched with user defined workload scenarios using custom FPGA images that couple CPU cores with a variety of accelerates emulated on the ZCU102 platform. 
- Discussions and Interactive Experimentation on the Fly (15 minutes) 
  - We will explore some of the scenarios listed below based on the interests of the audience:  
    - Experiment with a new applications that rely on key computation kernels such as FFT, GEMM, Convolution, Vector addition or Vector multiplication.  
    - Experiment with a new applications that require a new API call not supported by CEDR 
    - Walk through the integration of new API call to CEDR and perform functional verification on an x86 based system 


## Archival materials:

Click [here](./tutorial) for a self-paced, archival version of our tutorial workflow.
