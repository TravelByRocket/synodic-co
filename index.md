---
width: full
navbar:
  sticky: true
  scroll_up: true
  animation: true
  transparent: true
---

[comment]: # (This actually is the most platform independent comment)

{% if site.template == 'base' %}

  {% include portfolio.html 
    section_size="small"
    section_header_align="center"
    grid="1-2"
  %}
  
{% else %}


{% endif %}