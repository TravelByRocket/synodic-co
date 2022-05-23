---
width: full
navbar:
  sticky: false
  scroll_up: true
  animation: true
  transparent: false
---

[comment]: # (This actually is the most platform independent comment)

{% if site.template == 'base' %}

  {% include portfolio.html 
    section_size="small"
    section_header_align="center"
    grid="1-1"
    section_background="primary"
  %}
  
{% else %}


{% endif %}