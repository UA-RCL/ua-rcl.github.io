---
title: FPGA'25 Tutorial Introduction
style: /_styles/presentations/fpga24/custom.css
---

# CEDR: A Holistic Software and Hardware Design Environment for Hardware Agnostic Application Development and Deployment on FPGA-Integrated Heterogeneous Systems

<b>Overview:</b> As the FPGAs are being embedded in all layers of computing infrastructure from edge to HPC scale, system designers continue to explore design methodologies that leverage increased levels of heterogeneity to push performance within the target performance goals or constraints. In line with this objective, we have developed CEDR, —an open-source, unified compilation, and runtime framework designed for FPGA-integrated heterogeneous systems, as part of the DARPA DSSoC program. Our framework empowers users to seamlessly develop, compile, and deploy applications on off-the-shelf heterogeneous computing platforms. Importantly, this framework is portable across a wide range of Linux-based systems, ensuring that effort to migrate across systems is minimal. This tutorial builds upon the educational class we conducted on the open-source CEDR framework during ESWEEK’23 and the CEDR tutorial we delivered in ISFPGA’24, with a particular focus on FPGA-integrated heterogeneous systems. Our aim is to engage participants with our framework through hands-on exercises, facilitate interaction with FPGA-based SoCs, and foster productive discussions around challenges in heterogeneous computing.

CEDR is currently being leveraged in basic research as part of the DARPA SpaceBACN and DARPA PROWESS programs. Its utility has been validated through a diverse set of real-world applications by General Dynamics, Collins Aerospace, and the Johns Hopkins Applied Physics Laboratory, alongside several academic collaborators. Additionally, it has undergone independent evaluation by the Carnegie Mellon University Software Engineering Institute, further affirming its effectiveness. With its easy-to-use Application Programming Interface (API)-based programming model, CEDR has extended support and compatibility across programming models (GNURadio, PyTorch) and architectures (RISC-V, GPU, and ARM-based SoCs), making it a highly versatile runtime for heterogeneous computing. In our previous tutorial at ISFPGA’24, participants gained hands-on experience with CEDR’s API-based programming model. They successfully implemented a basic application and analyzed performance variations under different workload scenarios and scheduling heuristics—all within three hours. For users to be able to replicate the entire tutorial independently, we provided resources and step-by-step instructions on our dedicated page: [https://ua-rcl.github.io/presentations/fpga24/index.html](https://ua-rcl.github.io/presentations/fpga24/index.html)

For the 2025 edition of this tutorial, our goal is to deliver a comprehensive learning experience that builds on the foundational CEDR knowledge shared last year. The tutorial will begin with a refresher on the basics of CEDR, followed by an in-depth, hands-on exploration of advanced topics. Participants will learn to integrate new accelerators and APIs into the runtime, as well as apply fine-grained performance monitoring and profiling techniques on FPGA-based heterogeneous platforms. This approach aims to reduce the knowledge barrier for attendees, enabling them to develop and optimize applications using CEDR across various application domains and hardware platforms. In the final segment of the tutorial, we will preview the latest advancements in CEDR and introduce its new features for the users.

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

## Tutorial Structure and Flow
The tutorial is structured into two core exercises, each including a series of hands-on activities tailored to the needs of three distinct user types: naïve application developers, system designers, and resource management heuristic developers. Throughout these activities, the common thread is lifting the barriers to research and enabling productive application development and deployment on FPGA-integrated heterogeneous systems. The tutorial adopts a hands-on approach utilizing the Zynq UltraScale+ MPSoC ZCU102 Evaluation Kit, enabling participants to gain practical experience on systems that amalgamate ARM CPU cores with FPGA accelerators. 

### Schedule (150  minutes):

- Downloading and building CEDR (5 min)  
- CEDR Overview and capabilities (15 min) 
- Core Exercise 1 (75 minutes) 
  - <b>Part-1 [Naïve application developer, System designer]:</b> In this exercise, participants will walk through the basic setup, perform functional verification, and conduct performance analysis to harness FPGA-based acceleration. They will modify a reference C/C++ Radar Correlator implementation by integrating the CEDR FFT API, then compile and deploy the application on a ZCU102 platform configured with two FFT accelerators and four ARM CPU cores.  
    - <b>Activity-1 [Naïve application developer]:</b> Participants will deploy a single instance of the Radar Correlator and perform an end-to-end functional verification.
    - <b>Activity-2 [System designer]:</b> Participants will stress-test the scheduler by deploying multiple instances of the Radar Correlator, performing timing analysis, and visualizing how API calls are dispatched to compute units based on the selected scheduling heuristic. They will learn to set up experiments by tuning key parameters such as application arrival rate, hardware composition, and scheduling heuristic. Additionally, participants will utilize built-in scripts to collect log files and visualize the execution profile, gaining deeper insights into system behavior and performance.
  - <b>Part-2 [Resource management heuristic developer]:</b>

    The tutorial will guide participants on introducing a new API call to CEDR, performing functional verification, and deploying it on the ZCU102 using a pre-configured SoC image.
    - <b>Activity-1:</b> Introduce ZIP API call to CEDR, modify Radar Correlator application using the new ZIP API call, compile and execute on an X86-based setup to perform functional verification with the new API call.
    - <b>Activity-2:</b> Using a pre-generated FPGA image of an SoC configured with four ARM CPU cores, two FFT accelerators, and one ZIP accelerator, participants will deploy single and multiple instances of the new Radar Correlator implementation and conduct timing analysis as in Part 1, Activity 2.
- Core Exercise 2 (30 minutes)
  - With the ability to develop and deploy applications on an FPGA-based SoC established, this phase of the tutorial will focus on design space exploration. Participants will analyze systems composed of ARM CPUs and FPGA accelerators, gaining insights into performance trade-offs and optimization opportunities.
  - <b>Activity [System designer]:</b> Participants will learn to use the profiling scripts provided with CEDR to collect performance counter data, power consumption traces, and log files. They will conduct experiments by varying the number of compute resources and exploring different scheduling heuristics under dynamically arriving workload scenarios. These activities will leverage pre-built custom FPGA images that integrate CPU cores with various accelerators, all emulated on the ZCU102 platform.
- Pre-release CEDR 2.0 (25 minutes)
  - <b>Explore Recent Advancements:</b> Walk participants through the latest advancements in CEDR, which have achieved an 86x reduction in runtime overhead. 
  - <b>Introduce New Features in CEDR 2.0:</b> Present the enhanced capabilities of CEDR 2.0, including improvements in user productivity and performance gains enabled by OpenMP-based API parallelization.
  - <b>Interactive Discussion:</b> Engage attendees in a discussion about the new features of CEDR, gathering feedback and exploring potential applications and enhancements.


## Archival materials:

<!---
Click [here](./tutorial) for a self-paced, archival version of our tutorial workflow.
--->
<b>Hardware Images:</b> FPGA image used in this tutorial is available [here]("https://github.com/UA-RCL/Hardware-Images/tree/ZedBoard-ISFPGA25").

<b>Step-by-step Tutorial:</b> A self-paced, archival version of our tutorial workflow will be available here.
