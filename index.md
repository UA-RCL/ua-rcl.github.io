---
---

# University of Arizona Reconfigurable Computing Lab (UA-RCL)

***Our work sits at the intersection of computer architecture, system software, and domain-specific computing. We build the runtimes, compilers, schedulers, and hardware architectures that allow heterogeneous computing systems to be programmed, managed, and optimized in a unified, portable, and hardware-agnostic way from the embedded edge to high-performance platforms. If you want to see what it looks like when hardware diversity becomes a feature instead of a burden, explore our projects.***

Monolithic systems are architecturally rigid, making them poorly suited to diverse and dynamically evolving workloads. In such environments, execution efficiency and adaptability matter more than raw compute density. Heterogeneous architectures address this need by combining the complementary strengths of multiple computation models. Systems that couple CPUs with accelerators such as GPUs and FPGAs have already become mainstream, and the trajectory is clear. Architectures are evolving toward deeper heterogeneity with the integration of specialized processing elements such as NPUs, TPUs, and CGRAs. Yet as heterogeneity increases, so does complexity.

Researchers and system architects face mounting challenges in exploring the vast design space of processing element compositions, scheduler heuristics, and runtime strategies, and the tools needed to do so in a unified environment simply do not exist. Another critical challenge is in optimizing performance without sacrificing programming productivity, and the software and runtime infrastructure needed to harness this diversity remains fragmented, architecture-specific, and largely inaccessible. The UA-RCL exists to close this void.

{%
  include button.html
  type="github"
  text="RCL GitHub"
  link="UA-RCL"
%}

{% include section.html %}

## News
1. Mustafa Ghanim and Serhan Gener presented a poster and demo at the 2026 Big Idea Challenge Research 
Showcase as members of the AZSCI team. (Check out our [blog post](./2026/05/08/azsci.html))
1. Our paper titled ***Event-based Human Action Recognition: Rehabilitation Monitoring Dataset and Models***  is published in International Conference on Future Machine Learning and Data Science [(FMLDS'25)](https://www.fmlds.org/). This paper is available on ([IEEE Xplore](https://ieeexplore.ieee.org/document/11446492)).
1. Our paper titled ***K-PACT: Kernel Planning for Adaptive Context Switching — A Framework for Clustering, Placement, and Prefetching in Spectrum Sensing*** is published in International Conference on Computer-Aided Design ([ICCAD'25](https://2025.iccad.com/)). The paper is available on ([IEEE Xplore](https://ieeexplore.ieee.org/document/11240855)) and the source code is hosted on [Github](https://github.com/UA-RCL/K-PACT).
1. Our paper titled ***A Portable Framework with Generalized Runtime Features for Task Graph Execution and Concurrent Multi-Application Deployment on Heterogeneous Systems*** ([Science Direct](https://www.sciencedirect.com/science/article/pii/S0167739X25004789)) is published in Future Generation Computer Systems as journal preproof.
1. Our paper titled ***HOPPERFISH: Holistic Profiling with Portable Extensible and Robust Framework Intended for Systems with Heterogeneity***  is accepted for publication in ACM Transactions on Architecture and Code Optimization and is available as *just accepted* in [ACM](https://dl.acm.org/doi/abs/10.1145/3769087). The source code is hosted on [Github](https://github.com/UA-RCL/CEDR/tree/hopperfish).
1. Our paper titled ***An Overview of Challenges and Requirements for Real-Time Spectrum Sensing in Modern RF Autonomy Systems*** ([IEEE Xplore](https://ieeexplore.ieee.org/document/11104816)) is published in IEEE Design & Test.
1. Our paper titled ***RIMMS: Runtime Integrated Memory Management System for Heterogeneous Computing*** is accepted for publication in Embedded Systems Week ([ESWEEK'25](https://esweek.org/)) and is available as *just accepted* in [ACM](https://doi.org/10.1145/3760257) Transactions on Embedded Computing Systems as part of ESWEEK'25 special issue.
1. Our paper titled ***A Unified Portable and Programmable Framework for Task-Based Execution and Dynamic Resource Management on Heterogeneous Systems*** ([ACM](https://dl.acm.org/doi/10.1145/3720555.3721988)) was published in Extreme Heterogeneity Solutions ([ExHET'25](https://ornl.github.io/events/exhet2025/)). 
1. Our paper titled ***A Unified Portable and Programmable Framework for Task-Based Execution and Dynamic Resource Management on Heterogeneous Systems*** has won the Best Paper Award in Workshop on Extreme Heterogeneity Solutions ([ExHET'25](https://ornl.github.io/events/exhet2025/))! Congratulations Serhan! (Check out our [blog post](./2025/03/03/isfpga_tutorial_and_exhet.html))
1. Serhan Gener and Sahil Hassan held a Tutorial Session titled ***CEDR: A Holistic Software and Hardware Design Environment for Hardware Agnostic Application Development and Deployment on FPGA-Integrated Heterogeneous Systems*** in [ISFPGA'25](https://www.isfpga.org/workshops-tutorials/#t6). (Check out our [blog post](./2025/03/03/isfpga_tutorial_and_exhet.html)).
<!-- 1. Our paper titled ***A Unified Portable and Programmable Framework for Task-Based Execution and Dynamic Resource Management on Heterogeneous Systems*** is accepted for publication in Workshop on Extreme Heterogeneity Solutions ([ExHET'25](https://ornl.github.io/events/exhet2025/)) -->
1. Our paper titled ***A Runtime Manager Integrated Emulation Environment for Heterogeneous SoC Design with RISC-V Cores*** ([IEEE Xplore](https://ieeexplore.ieee.org/document/10596355)) was published in Heterogeneity in Computing Workshop ([HCW'24](https://hcw.pages.dev/)). 
   

Click [here](./archived_news/) to check out archived news.

## Open-Source Highlights
{% include open_source_grid.html %}

## Highlights

{% capture text %}

Click the link below for our active and archived projects.

{%
  include button.html
  link="projects"
  text="Browse our projects"
  icon="fa-solid fa-arrow-right"
  flip=true
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/RCL_areas.png"
  link="projects"
  title="Our Projects"
  text=text
%}

{% capture text %}

Click the link below to meet our team members.

{%
  include button.html
  link="team"
  text="Meet our team"
  icon="fa-solid fa-arrow-right"
  flip=true
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/blog/picacho_peak/picacho1.jpeg"
  link="team"
  title="Our Team"
  flip=true
  style="bare"
  text=text
%}

<!-- 
Will uncomment as the tutorial is finalized

{% capture text %}

Click the link below to see our presentations and tutorials.

{%
  include button.html
  link="presentations"
  text="Presentations and Tutorials"
  icon="fa-solid fa-arrow-right"
  flip=true
  style="bare"
%}

{% endcapture %}

{%
  include feature.html
  image="images/blog/picacho_peak/picacho1.jpeg"
  link="presentations"
  title="Our Presentations"
  style="bare"
  text=text
%} -->
