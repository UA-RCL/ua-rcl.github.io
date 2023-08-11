---
title: Research
nav:
  order: 1
  tooltip: Published works
---

# {% include icon.html icon="fa-solid fa-microscope" %}Research

{% include section.html %}

# Domain-Focused Advanced Software-Reconfigurable Heterogeneous System on Chip (DASH-SoC)

**Funded by**: DARPA

**Collaborators**: Arizona State University, University of Michigan, Carnegie Mellon

**Students**: Joshua Mack, Sahil Hassan, Serhan Gener, Mustafa Ghanim, H. Umut Suluhan

The DASH-SoC team solves critical challenges, which include identifying the appropriate SoC capabilities and simplifying system implementations. We develop intelligent design-time and real-time tools to improve SoC throughput, latency, power efficiency, and flexibility. We promote the use and development of open tools to enable broader applicability. We develop intelligent algorithms that identify the underlying ontologies of a set of important applications that include communications, radars, and SIGINT, and translate this information to specific application-domain SoC architectures, including processing element (PE) specification. We dramatically extend current compiler and debugging tools to address the needs of heterogeneous SoCs. We develop an innovative dynamic intelligent scheduler (IS), which learns from observing needs and performance metrics, to remove the requirement for domain-expert tuning of threading. In tight coordination with the IS and software tools, we design sophisticated on-chip media-access-control (MAC) capabilities that enable on-chip communications to the PEs.

Please refer to [Compiler-Integrated Emulation Environment and DSSoC Runtime (CEDR)](../projects/cedr) project page for current state of the project.

# Neuromorphic Computing

**Funded by**: Raytheon

**Collaborator**: Air Force Research Labs

**Students**: Joshua Mack, Nirmal Kumbhare, Edward Richter, Ruben Purdy, Spencer Valancius, John Mixter

### Applications and Architectures of Neuromorphic Computing

In this project we are building an open source C++ software simulation and Field Programmable Gate Array (FPGA) emulation environment of the TrueNorth architecture. These technologies will provide a flexible hardware framework for neuromorphic architectural research to:

- further understand the TrueNorth architecture design decisions
- make TrueNorth architecture accessible for researchers and application developers through a programming and testing environment
- enable researchers to feasibly alter architectural features and investigate the relationship between network parame
ters (training methods, binary spikes, thresholds, leak values, synaptic weights) and performance metrics (classification accuracy and energy efficiency).

To the best of our knowledge there is no such flexible hardware platform publicly available to perform design space exploration on neuromorphic architectures for deep learning research. The source code for our software simulation is available here

Please refer to [Reconfigurable Architecture for Neuromorphic Computing (RANC)](../projects/ranc) project page for current state of the project.

# HPC Productivity and Cloud Resource Management

**Funded by**: NSF (I/UCRC Cloud and Autonomic Computing)

**Collaborator**: H. J. Siegel (Colorado State University), Aniruddha Marathe and Ghaleb Abdulla ( Lawrence Livermore National Laboratory) )

**Researchers**: Nirmal Kumbhare

Data infrastructures such as Google, Amazon, eBay, and E-Trade are powered by data centers (DCs) that contain tens to hundreds of thousands of computers and storage devices running complex software applications. Between 2013 to 2020, organizations’ investment in software for mobile, social, cloud, and big data technologies is expected to grow over 20 times faster than organizations’ investment in hardware for Information Technologies (IT) Traditional IT architectures are not designed to provide an agile infrastructure to keep up with the rapidly evolving next-generation mobile, big data, and application demands, as they are distinct from the “traditional” enterprise applications. Common characteristics of the next-generation applications are nonlinear scaling and relatively unpredictable growth as a function of inputs being processed, their size, and dynamic behavior. The dynamic and unpredictable changes in the Service Level Objectives (SLOs) (e.g., availability response time, reliability, energy) of these applications require continuous provisioning and re-provisioning of DC resources. Ultimately, this means considering the impractical approach of building new DCs that can efficiently support the distinct design principles for each unique DC workload or application. The goal of our research is to design an innovative composable “Just in Time Architecture (JITA)” DC and associated resource management techniques that utilize a set of flexible building blocks that can be dynamically and automatically assembled and re-assembled to meet the dynamic changes in workload’s SLO of current and future DC applications. Towards enabling the design of Just In Time Architectures (JITA) for the next generation DC applications we focus on addressing the dynamic composition and resource management challenges by building a Virtual DC and investigating:

- Novel application-aware DC management system to monitor and analyze the execution of the DC resources continuously, control the logical and physical resource components dynamically, and re-configure them automatically to meet its SLOs at runtime
- Novel model driven resource management heuristics and scheduling algorithms based on time dependent metrics that measure the value of a service to achieve a balance between competing goals (e.g., completion time and energy consumption).

In order to measure HPC productivity, we utilize a monotonically decreasing time-dependent value function that represents the value of completing the job for an organization. We quantify HPC productivity by accumulating the job-values achieved by the completed jobs. We then leveraged VoS as the basis for constructing power-aware value-based scheduling algorithms [7] in order to improve productivity of a power-constrained and oversubscribed HPC system. First one distributes the system power uniformly among the nodes to improve node utilization, second one allocates power in a greedy manner to high value jobs to meet their timing requirements. We study these two algorithms under different system-wide power-constraints on a real HPC prototype using synthetic workload trace of real scientific routines.

Please refer to [Productivity-Aware Scheduling in HPC (PASH)](../projects/pash) project page for current state of the project.

# Adaptable Low Density Parity Check (LDPC) Engine

**Researchers**: Sahil Hassan

Algorithmic Contribution: We introduced a new algorithm called Probabilistic Gallagher B (PGaB) by applying a probabilistic stimulation function over the iterative decoding process, conduct detailed experimental evaluations with respect to other decoders and show that our algorithm not only improves the decoding performance with respect to GaB by four orders of magnitude, but also requires fewest amountof hardware resources with respect to other comparable decoding algorithms GDBF and PGDBF while achieving equivalent or better decoding performance. We present the details of our incremental approach to designing and implementing the GaB and PGaB hardware architecture.

Architecture Specific Contribution: The connection intensive bipartite graph based LDPC decoder hardware architecture creates routing stress when implemented on the FPGA for longer codewords that are utilized in today's communications systems and standards. From FPGA point of view, even though there is sufficient amount of computing resources that would match the degree of parallelism desired by the design, implementation is less likely to pass the routing stage of the synthesis as the number of connections in the implementation increase with the code length, which in turn increases the stress on FPGA routing resources. Another contributor to the routing stress is the number of parity bits used by the communication medium, which has direct impact on the number of connections between each iteration of the decoding process since increasing the ratio of parity bit to data from 0.5 to 0.75 would mean increasing number of connections by a factor of 4 for a given codeword. Therefore for implementations of longer codewords and/or higher code rates, designers resort to reducing the degree of parallelism in their implementations.

Please refer to [LDPC Simulation Testbed (LDPC)](../projects/ldpc) project page for current state of the project.

{% include section.html %}

