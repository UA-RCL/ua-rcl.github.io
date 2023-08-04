---
title: Team
nav:
  order: 3
  tooltip: About our team
---

# {% include icon.html icon="fa-solid fa-users" %}Team

Go to team/index.md to modify this. Everyone should edit their pages from /members folder to make sure everything is correct. 

Are we going to add previous members??

{% include section.html %}

{% include list.html data="members" component="portrait" filters="role: pi" %}<br>
{% include list.html data="members" component="portrait" filters="role: phd" %}

{% include section.html background="images/background.jpg" dark=true %}

Go to team/index.md to modify here

{% include section.html %}

## GRADUATED

{% include list.html data="members" component="portrait" filters="role: graduated" %}<br>


- Alex Fusco (MS) Spring 2023, @ SpaceX <br>
    Hardware-based resource management for heterogenous SoCs
- PArker Dattilo (MS) Spring 2023, @ Raytheon <br>
    Error correction on neuromorphic computing architectures
- Nirmal Kumbhare (Ph.D.) Spring 2019, @ Apple <br>
    Power-Aware Value-Based Resource Management in High Performance Computing Systems
- Burak Unal (Ph.D.) Spring 2019, Assistant Professor @ Karabuk University, Turkey <br>
    Low-Density Parity-Check Code Decoder Design and Error Characterization on an FPGA Based Framework
- Elnaz T. Yazdi (MS) Fall Spring 2018, @ Photometrics <br>
    Developing A Highly Parallelized TCR Synthesis Algorithm on GPGPU and FPGA For Accelerating the Study of Immune Systems

| TABLE | Game 1 | Game 2 | Game 3 | Total |
| :---- | :----: | :----: | :----: | ----: |
| Anna  |  144   |  123   |  218   |  485  |
| Bill  |   90   |  175   |  120   |  385  |
| Cara  |  102   |  214   |  233   |  549  |

We can also have a table like above but it doesn't look good and harder to maintain


{% capture content %}

{% include figure.html image="images/photo.jpg" %}
{% include figure.html image="images/photo.jpg" %}
{% include figure.html image="images/photo.jpg" %}

{% endcapture %}

{% include grid.html style="square" content=content %}
