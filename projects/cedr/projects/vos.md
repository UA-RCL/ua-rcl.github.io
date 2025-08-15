---
layout: cedr_layout
title: Value of Service
---

# Value based Runtime Management

Value-based resource management heuristics, which are traditionally deployed in heterogeneous HPC systems, maximize system productivity by assigning resources to each job based on its priority and estimated value gain relative to each job's completion time. We investigate the utility of value-based resource management at heterogeneous SoC scale and demonstrate its ability to make effective scheduling decisions for time-constrained jobs in oversubscribed systems where system resources are shared by multiple users and applications arrive dynamically. The proposed value-based resource management approach drops tasks that are estimated to result with lower-value gain dynamically with the aim of completing more number of high-value jobs with a scheduling decision time at 120𝜇s scale. The value-based resource management treats scheduling as a global optimization problem, therefore this study sets a path forward for deploying a unified value-based resource management on a system composed of front-end SoC-based edge devices and a back-end HPC system.