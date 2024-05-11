---
title: FPGA'24 Tutorial Introduction
style: /_styles/presentations/fpga24/custom.css
---

# Seamless and Rapid PyTorch Model Deployment in Heterogeneous SoC

When designed with the right mix of accelerators and general-purpose processors, heterogeneous systems offer performance and energy efficiency not attainable with homogeneous counterparts. Optimizing a heterogeneous computing system is a multi-dimensional and complex design space exploration problem particularly in scenarios where algorithms, data types, and processing resources and their availability vary dynamically. In this study, our aim is to design and develop an intelligent runtime framework that enables deployment of machine learning models on heterogeneous computing systems under dynamically arriving workload scenarios. The proposed framework offers the ability to adjust the composition of the data processing pipeline to align with the desired configuration of associated machine learning workflows through model-driven resource management heuristics; and streamlining data transfers for each workflow by continuously provisioning and re-provisioning resources (compute, memory) in a closed loop fashion through low-overhead, non-intrusive resource state monitoring mechanisms.

We realize seamless deployment of PyTorch models by dynamically loading accelerator-supported functions during runtime. This approach allows runtime to benefit from accelerators for certain layers and fall back to CPU for unsupported layers. Such flexibility facilitates the integration from native Python implementation to a diverse set of heterogeneous SoCs. Numerous methods have been introduced for deploying machine learning models on FPGA platforms leveraging Open Neural Network Exchange (ONNX) or PYNQ. While these methods alleviate the developer’s workload, they necessitate hardware expertise during the implementation process and lack seamless endto-end integration. In contrast, our approach does not require users to have prior FPGA-based design experience and delivers a straightforward, portable, and adaptable deployment process. This is achieved by incorporating neural
network layers at the task level through an API-based programming model, thereby obviating the necessity for hardware implementation of the model. We demonstrate proposed framework’s capabilities through preliminary studies by deploying PyTorch models on heterogeneous SoCs such as Xilinx Zynq UltraScale+™ MPSoC ZCU102 and NVIDIA Jetson AGX Xavier. We showcase the impact of scheduling heuristic and hardware configurations on the system’s performance under dynamic workloads leveraging the FPGA-based MPSoC. This framework provides application developers with the flexibility of deploying their neural networks on platforms other than GPUs and enables them to realize machine learning execution on power-constrained environments while taking advantage of the parallelism offered by FPGA-based compute platforms without having to program in their native programming models.

Click [here](./posters/PyTorch.pdf) to see our poster from IPDPS PhD Forum.

{%
  include portrait.html
  name="Umut Suluhan"
  description="Umut Suluhan is a second year PhD student in the Reconfigurable Computing Lab. His research interests are broadly in high-performance computing and reconfigurable architectures with a focus on runtime software design for domain specific system on chips and resource management in heterogeneous computing systems."
  image="/images/profiles/lab/umut_suluhan.jpg"
  custom-class="wide-profile"
%}

{% 
  include portrait.html
  name="Ali Akoglu"
  description="Ali Akoglu is a professor in the Department of Electrical and Computer Engineering and the BIO5 Institute at the University of Arizona.He is the site director of the National Science Foundation (NSF), Industry-University Cooperative Research Center on Cloud and Autonomic Computing."
  image="/images/profiles/lab/ali_akoglu.jpg"
  custom-class="wide-profile"
%}

