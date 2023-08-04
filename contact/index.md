---
title: Contact
nav:
  order: 5
  tooltip: Email, address, and location
---

# {% include icon.html icon="fa-regular fa-envelope" %}Contact

Go to contact/index.md to modify here.

{%
  include button.html
  type="email"
  text="akoglu@arizona.edu"
  link="akoglu@arizona.edu"
%}
{%
  include button.html
  type="phone"
  text="(520) 626-5149"
  link="+1-520-626-5149"
%}
{%
  include button.html
  type="address"
  text="ECE356B"
  tooltip="Our location on Google Maps for easy navigation"
  link="https://www.google.com/maps/place/Department+of+Electrical+and+Computer+Engineering/@32.2356201,-110.9534426,15z/data=!4m2!3m1!1s0x0:0x9a1073d0b9a5bc24?sa=X&ved=2ahUKEwiI5_Tmh8KAAxVLLUQIHeqTB7AQ_BJ6BAhSEAA&ved=2ahUKEwiI5_Tmh8KAAxVLLUQIHeqTB7AQ_BJ6BAhgEAg"
%}

{% include section.html %}

{% capture col1 %}

{%
  include figure.html
  image="images/uofa.webp"
%}

{% endcapture %}

{% capture col2 %}

{%
  include figure.html
  image="images/storyHero.jpg"
  caption="University Of Arizona - ECE Department"
%}

{% endcapture %}

{% include cols.html col1=col1 col2=col2 %}

{% include section.html dark=true %}

{% capture col1 %}
Lorem ipsum dolor sit amet  
consectetur adipiscing elit  
sed do eiusmod tempor
{% endcapture %}

{% capture col2 %}
Lorem ipsum dolor sit amet  
consectetur adipiscing elit  
sed do eiusmod tempor
{% endcapture %}

{% capture col3 %}
Lorem ipsum dolor sit amet  
consectetur adipiscing elit  
sed do eiusmod tempor
{% endcapture %}

{% include cols.html col1=col1 col2=col2 col3=col3 %}
