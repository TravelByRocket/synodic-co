---
width: full
navbar:
  sticky: true
  scroll_up: true
  animation: true
  transparent: true
  transparent_color: light
header:
  layout: 1-1 # Options: left, center, 1-1, 1-2, 1-3 or 2-3
  background_image: Working-Space.jpg
  background_video: Working-Space.mp4
  background_overlay: "linear-gradient(to left top,rgba(218, 91, 197, 0.8) 0%,rgba(151, 27, 191, 0.8) 30%,rgba(2, 8, 212, 0.8) 80%)"
  color: light
  heading_size: medium
  height: full
  parallax: true
  container: small
  content:
    block: header-home
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