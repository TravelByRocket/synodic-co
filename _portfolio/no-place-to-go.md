---
title: No Place to Go
subtitle: Companion app for a socially distanced haunted house in October 2020
image: no-place-to-go/mockup.png
topics: []
width: full
navbar:
  sticky: false
  transparent: false
  transparent_color: light
header:
  layout: center # Options: center 1-2 or 2-3
  background_overlay: "#191919"
  color: light
  header_size: small
  parallax: true
---

{% include block.html 
  block="no-place-to-go"
  section_size="xsmall"
  section_container="small"
  section_header_align="center"
  section_background="primary"
  section_content_align="center"
  block_title="false"
%}

{% include image.html 
  src="no-place-to-go/mockup.png"
  alt="Screenshot and mockup of app home screen"
  section_size="medium"
  section_background="primary"
  section_container="medium"
%}

{% include gallery.html 
	grid="1-3"
	gallery="no-place-to-go/gallery"
	caption="true"
	lightbox="true"
  section_size="small"
  section_background="primary"
  section_padding_remove="top"
%}