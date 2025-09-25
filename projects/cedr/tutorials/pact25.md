---
layout: cedr_layout
title: PACT'25
order: 4
---

# CEDR: A Holistic Software and Hardware Design Environment for Hardware Agnostic Application Development and Deployment on FPGA-Integrated Heterogeneous Systems

<b>Overview:</b> As the FPGAs are being embedded in all layers of computing infrastructure from edge to HPC scale, system designers continue to explore design methodologies that leverage increased levels of heterogeneity to push performance within the target performance goals or constraints. In line with this objective, we have developed CEDR, —an open-source, unified compilation, and runtime framework designed for FPGA-integrated heterogeneous systems, as part of the DARPA DSSoC program. Our framework empowers users to seamlessly develop, compile, and deploy applications on off-the-shelf heterogeneous computing platforms. Importantly, this framework is portable across a wide range of Linux-based systems, ensuring that effort to migrate across systems is minimal.  This tutorial builds upon the education class we conducted on the open-source CEDR framework during ESWEEK’23. Since then, CEDR has matured substantially, and we have shared it with the community through interactive tutorials in ISFPGA’24 and ISFPGA’25. For PACT'25, we have partnered with AMD to deliver the participants with a seamless engagement experience with our framework through hands-on exercises, interaction with FPGA-based SoCs, and productive discussions around challenges in heterogeneous computing.

CEDR is currently being leveraged in basic research as part of the DARPA SpaceBACN and DARPA PROWESS programs. Its utility has been validated through a diverse set of real-world applications by General Dynamics, Collins Aerospace, and the Johns Hopkins University Applied Physics Laboratory, alongside several academic collaborators. Additionally, it has undergone independent evaluation by the Carnegie Mellon University Software Engineering Institute, further affirming its effectiveness. With its easy-to-use Application Programming Interface (API)-based programming model, CEDR has extended support and compatibility across programming models (GNURadio, PyTorch) and architectures (RISC-V, GPU, and ARM-based SoCs), making it a highly versatile runtime for heterogeneous computing. In our latest tutorial at ISFPGA’25, participants gained hands-on experience with CEDR’s API-based programming model. They successfully implemented a basic application and analyzed performance variations under different workload scenarios and scheduling heuristics on ARM-based heterogeneous SoC emulated on FPGA—all within three hours. For users to be able to replicate the entire tutorial independently, we provided resources and step-by-step instructions on our dedicated page: [https://ua-rcl.github.io/projects/cedr/tutorials/step-by-step/fpga25_tutorial/](https://ua-rcl.github.io/projects/cedr/tutorials/step-by-step/fpga25_tutorial/)

For this edition of the tutorial, our goal is to deliver a comprehensive learning experience that builds on the foundational CEDR knowledge shared during the previous education class and tutorials. This tutorial aims to leverage the tested and proven stable learning environment of its precursors, while further improving the practical, hands-on learning experience using AMD’s hardware platform. The tutorial will begin with a refresher on the basics of CEDR, followed by an in-depth, hands-on exploration of advanced topics. Participants will learn to integrate new accelerators and APIs into the runtime, as well as apply fine-grained performance monitoring and profiling techniques on FPGA-based heterogeneous platforms, provided by AMD. This approach aims to reduce the knowledge barrier for attendees, enabling them to develop and optimize applications using CEDR across various application domains and hardware platforms. In the final segment of the tutorial, we will preview the latest advancements in CEDR and introduce its new features for the users.

<div style="display: flex; gap: 2rem; justify-content: center; align-items: flex-start;">
{%
  include portrait.html
  name="Sahil Hassan"
  description="Sahil Hassan is a Post-Doc in the Reconfigurable Computing Lab graduating since Spring 2024. His research interests include design and development of resource management techniques for emerging heterogeneous embedded computing systems, novel architectures and algorithms for neuromorphic computing, and FPGA based reconfigurable architectures."
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
</div>

## Tutorial Structure and Flow
The tutorial is structured in a half-day format that covers two core exercises, each including a series of hands-on activities tailored to the needs of three distinct user types: application developers, system designers, and resource management heuristic developers. Throughout these activities, the common thread is lifting the barriers to research and enabling productive application development and deployment on FPGA-integrated heterogeneous systems. The tutorial adopts a hands-on approach utilizing the AMD Xilinx FPGA platforms, enabling participants to gain practical experience on systems that amalgamate ARM CPU cores with FPGA accelerators.

### Schedule (180  minutes):

- Downloading and building CEDR (5 min)  
- CEDR Overview and capabilities (15 min) 
- Core Exercise 1 (110 minutes):
  - <b>Part-1 [All three user types]:</b> In this exercise, participants will walk through the basic setup, perform functional verification, and conduct performance analysis to harness FPGA-based acceleration. They will modify a reference C/C++ Radar Correlator implementation by integrating the CEDR FFT API, then compile and deploy the application on an FPGA platform configured with two FFT accelerators and ARM CPU cores.
    - <b>Activity-1 [Application developer]:</b> Participants will deploy a single instance of the Radar Correlator and perform an end-to-end functional verification.
    - <b>Activity-2 [System designer, Resource management heuristic developer]:</b> Participants will stress-test the scheduler by deploying multiple instances of the Radar Correlator, performing timing analysis, and visualizing how API calls are dispatched to compute units.
  - <b>Part-2 [All three user types]:</b> The tutorial will guide participants on introducing a new API call to CEDR, performing functional verification, and deploying it on the FPGA. 
    - <b>Activity-1 [System designer, Resource management heuristic developer]:</b> Introduce ZIP API call to CEDR, modify Radar Correlator application using the new ZIP API call, compile and execute on an X86-based setup to perform functional verification with the new API. 
    - <b>Activity-2 [Application developer, System designer]:</b> Using a pre-generated FPGA image of an SoC configured with four ARM CPU cores, two FFT accelerators, and one ZIP accelerator, participants will deploy single and multiple instances of the new Radar Correlator implementation and conduct timing analysis as in Part 1, Activity 2.
- Core Exercise 2 (40 minutes)
  - With the ability to develop and deploy applications on an FPGA-based SoC established, this phase of the tutorial will focus on design space exploration. Participants will analyze systems composed of ARM CPUs and FPGA accelerators, gaining insights into performance trade-offs and optimization opportunities.
  - <b>Activity [System designer]:</b> Participants will learn to use the profiling scripts provided with CEDR to collect performance counter data, power consumption traces, and log files. They will conduct experiments by varying the number of compute resources and exploring different scheduling heuristics under dynamically arriving workload scenarios. These activities will leverage pre-built custom FPGA images that integrate CPU cores with various accelerators, all emulated on the ZCU102 platform. 
- Interactive Discussion (30 minutes)
  - <b>Explore Recent Advancements:</b> Walk participants through the latest advancements in CEDR, which have achieved an 86x reduction in runtime overhead. 
  - <b>Introduce New Features in CEDR 2.0:</b> Present the enhanced capabilities of CEDR 2.0, including improvements in user productivity and performance gains enabled by OpenMP-based API parallelization.
  - <b>Interactive Discussion:</b> Engage attendees in a discussion about the new features of CEDR, gathering feedback and exploring potential applications and enhancements.


## Archival materials:

<b>Hardware Images:</b> FPGA image used in this tutorial is available <a href="https://github.com/UA-RCL/Hardware-Images/tree/AUP-ZU3-2fft2zip" target="_blank">here</a>.

<b>Step-by-step Tutorial:</b> A self-paced, archival version of our tutorial workflow is available [here](/projects/cedr/tutorials/step-by-step/pact25_tutorial.html).
