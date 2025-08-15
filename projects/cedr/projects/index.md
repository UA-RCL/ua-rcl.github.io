---
layout: cedr_layout
title: CEDR Projects
---

# {% include icon.html icon="fa-solid fa-wrench" %} CEDR Projects

## Active

{% capture cards %}
  {% include list.html data="cedr_projects" component="card" filters="group: featured" %}
{% endcapture %}

<!--{% include grid.html content=cards %}-->
<div class="grid" data-style="{{ include.style }}">
  {{ cards | markdownify }}
</div>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr)); /* 250px is the minimum card width */
    gap: 1rem; /* spacing between cards */
    align-items: start;
  }
</style>