---
layout: cedr_layout
title: ISFPGA'26
order: 5
---

# CEDR: A Holistic Software and Hardware Design Environment for Hardware Agnostic Application Development and Deployment on FPGA-Integrated Heterogeneous Systems

<b>Overview:</b> As FPGAs are being embedded in all layers of computing infrastructure from edge to HPC scale, system designers continue to explore design methodologies that leverage increased levels of heterogeneity to push performance within the target performance goals or constraints. In line with this objective, we have developed CEDR, an open-source, unified compilation and runtime framework designed for FPGA-integrated heterogeneous systems, initially created as part of the DARPA DSSoC program. Our framework empowers users to seamlessly develop, compile, and deploy applications on off-the-shelf heterogeneous computing platforms. The framework is portable across a wide range of Linux-based systems, enabling seamless migration between platforms.  Building on the previous CEDR tutorials conducted at ESWEEK’23, ISFPGA’24, ISFPGA’25, ESWEEK’25, and PACT’25, this tutorial caters to audiences with diverse backgrounds and varying levels of expertise through hands-on activities tailored to three user types: application developers, system designers, and resource management heuristic developers.  For the 2026 edition, we partner with AMD to provide learning experience through hands-on exercises using AMD Xilinx FPGA-based SoCs and discussions around emerging challenges in heterogeneous computing. 

CEDR is currently being leveraged in basic research and its utility has been validated through a diverse set of real-world applications by General Dynamics, Collins Aerospace, and the Johns Hopkins University Applied Physics Laboratory, alongside several academic collaborators. Additionally, it has undergone independent evaluation by the Carnegie Mellon University Software Engineering Institute. With its easy-to-use Application Programming Interface (API)-based programming model, CEDR has extended support and compatibility across programming models (GNURadio, PyTorch, Taskflow) and architectures (RISC-V, GPU, FPGA, and ARM-based SoCs), making it a highly versatile runtime for heterogeneous computing. In recent tutorials at ISFPGA’25, ESWEEK’25, and PACT’25, participants gained hands-on experience with CEDR on implementing applications and analyzing performance across diverse workload scenarios and scheduling heuristics using FPGA-based heterogeneous SoCs. Through our partnership with AMD, attendees in ESWEEK’25 and PACT’25 executed their implementations directly on AMD’s AUP-ZU3 FPGA boards. To enable repeatability and independent learning, all tutorial materials, including step-by-step instructions, test applications, and reference FPGA images, are publicly available [https://ua-rcl.github.io/projects/cedr/tutorials/step-by-step/fpga26_tutorial.html](https://ua-rcl.github.io/projects/cedr/tutorials/step-by-step/fpga26_tutorial.html).

For this edition of the tutorial, our goal is to deliver a comprehensive learning experience that builds on the foundational CEDR content introduced in prior tutorials while significantly expanding the depth and hands-on scope. We devote more time to FPGA-level design space exploration (DSE), enabling participants to run full DSE experiments directly on the hardware. This structure lowers the learning barrier for attendees and equips them with the skills needed to efficiently develop, optimize, and deploy applications using CEDR across diverse application domains and SoC configurations. The tutorial will conclude with a preview of the latest advancements in CEDR, including newly introduced features and upcoming enhancements. We leverage the proven, stable learning environment refined through previous offerings and enhance it with expanded FPGA-focused activities using AMD’s hardware platform. The session will begin with a concise refresher on the fundamentals of CEDR, ensuring both new and returning participants can follow the material. From there, the tutorial will transition into advanced topics, including integrating new accelerators and APIs into the runtime and applying fine-grained performance monitoring and profiling techniques on AMD’s FPGA-based heterogeneous platforms.  

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
The tutorial is structured in a half-day format that covers two core exercises, each including a series of hands-on activities tailored to the needs of three distinct user types: application developers, system designers, and resource management heuristic developers. Throughout these activities, the common thread is to lower the barriers to research and enable productive application development and deployment on FPGA-integrated heterogeneous systems. The tutorial adopts a hands-on approach using AMD Xilinx FPGA platforms, enabling participants to gain practical experience with systems that combine ARM CPU cores with FPGA accelerators.

### Schedule (210  minutes):

- Downloading and building CEDR (5 min)  
- CEDR Overview and capabilities (15 min) 
- Core Exercise 1 (100 minutes) 
  - <b>Part-1 [Application developer, System designer, Resource management heuristic developer]:</b> In this exercise, participants will walk through the basic setup, perform functional verification, and conduct performance analysis to harness FPGA-based acceleration. They will modify a reference C/C++ Radar Correlator implementation by integrating the CEDR FFT API, then compile and deploy the application on an FPGA platform configured with two FFT accelerators and ARM CPU cores.
    - <b>Activity-1 [Application developer]:</b> Participants will deploy a single instance of the Radar Correlator and perform an end-to-end functional verification.
    - <b>Activity-2 [System designer, Resource management heuristic developer]:</b> Participants will stress-test the scheduler by deploying multiple instances of the Radar Correlator, performing timing analysis, and visualizing how API calls are dispatched to compute units.
  - <b>Part-2 [Application developer, System designer, Resource management heuristic developer]:</b> This exercise will guide participants in introducing a new API call to CEDR, performing functional verification, and deploying it on the FPGA.
    - <b>Activity-1 [System designer, Resource management heuristic developer]:</b> Introduce ZIP API call to CEDR, modify Radar Correlator application using the new ZIP API call, compile and execute on an X86-based setup to perform functional verification with the new API.
    - <b>Activity-2 [Application developer, System designer]:</b> Using a pre-generated FPGA image of an SoC configured with ARM CPU cores, two FFT accelerators, and one ZIP accelerator, participants will deploy single and multiple instances of the new Radar Correlator implementation and conduct timing analysis as in Part 1, Activity 2.
- Core Exercise 2 (60 minutes)
  - This phase of the tutorial will focus on design space exploration. Participants will analyze systems composed of ARM CPUs and FPGA accelerators, gaining insights into performance trade-offs.
  - <b>Activity [System designer]:</b> Participants will learn to use the profiling scripts provided with CEDR. They will conduct experiments by varying the number of compute resources and exploring different scheduling heuristics under dynamically arriving workload scenarios on the FPGAs.
- Pre-release CEDR 2.0 (30 minutes)
  - <b>Explore Recent Advancements:</b> Walk participants through the latest advancements in CEDR, which have achieved an 86x reduction in runtime overhead. 
  - <b>Introduce New Features in CEDR 2.0:</b> Present the enhanced capabilities of CEDR 2.0, including improvements in user productivity and performance gains enabled by OpenMP-based API parallelization.
  - <b>Interactive Discussion:</b> Engage attendees in a discussion about the new features of CEDR, gathering feedback and exploring potential applications and enhancements.

<b>Logistics:</b> Users will be given access to AMD’s FPGA-based SoC platforms, specifically the [AUP-ZU3 development board](https://www.amd.com/en/corporate/university-program/aup-boards/realdigital-aup-zu3.html). The tutorial page will be maintained at [CEDR Tutorials](https://ua-rcl.github.io/projects/cedr/tutorials/). All necessary FPGA images for various SoC configurations, along with test applications and step-by-step instructions for each activity, will be maintained and shared with the attendees using the tutorial page. To follow the tutorial, participants will need access to a native or virtual Linux machine with an internet connection. Alternatively, they can use a ready-to-run Docker image, which will be provided and compatible with Windows, Linux, and macOS platforms, or any platform that can run Docker. 

## Archival materials:

<b>Hardware Images:</b> FPGA image used in this tutorial is available <a href="https://github.com/UA-RCL/Hardware-Images/tree/AUP-ZU3-2fft2zip" target="_blank">here</a>.

<b>Step-by-step Tutorial:</b> A self-paced, archival version of our tutorial workflow is available [here](/projects/cedr/tutorials/step-by-step/fpga26_tutorial.html).
