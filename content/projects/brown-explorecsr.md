---
title: 'Brown ExploreCSR'
# date: 2023-11-18T15:47:40.000Z
draft: false
summary: "SVG creations from the exploreCSR program @Brown Spring 2023"
tags: ["svg","research","visual"]
cover:
  image: /img/projects/brown-explorecsr/svg_poster_Explore_CSR_Pearl_Zhang_Yuhan_Wang.png
  alt: Brown ExploreCSR SVG Poster
  hidden: false
author: ["Spring 2023"]
hideMeta: false
weight: 30
---

## Overview
Spring 2023, I joined the ExploreCSR program hosted by Brown University and Google Research. Together with Pearl Zhang, we were mentored by Prof. Jeff Huang and PhD candidate Catherine Chen, and explored the liability to use SVG images as web page background. SVG(Scalable Vector Graphics) images are vector-based. Instead of containing a grid of pixels with different color values, SVG images are a collection of line, curve, shape objects, that are very precise and also support animation. Moreover, SVG images can be coded directly under \<svg\> tags, which extends its flexibility to be embedded in html and to adjust to the screen accordingly.

<!-- some conclusion sentence-->


---
## SVG Creations
Here is a snippet of my SVG creations. They fall into differnet categories, and you can see that through iteration, I added more randomness, texture, and interaction in the images. 

{{< svg_showcase >}}


A main focus of our research is to test out the blurry effect and randomness of vector images, as we don't want backgrounds to be distracting, rather to offer a feeling, a tone. By implementing a css trick, we can include turbulence (noise) into the color and create a random dithering effect (like p5). Similarly, we can apply different extures like canvas pattern to the background. Another interesting discovery is to add random movements in the creations. Shadows and whitespace in images can produce visual illusions that adds moving depth to the background, which opens up new possibility for website interaction.

---
## User Study
In addition to using \<svg\>  tags to code images, we also investigated several online SVG generators, particularly filtered.ink, which is a work in progress in Prof.Jeff Huang's lab. filtered.ink, as suggested by its name, allows users to pick the effect they want and then directly draw out shapes that have embedded filtered color, animation, etc. As it is an untraditional way of making digital creations, Pearl and I conducted a user study where we each invited 10 students from our school with different academic and art background to learn about filtered.ink.

Based on our observation, the learning curve of filtered.ink is higher than usual tools, because of the flexibility and a wide range of options it offered.
<!--to be filled-->

---
## Poster Showcase
To conclude our discoveries and to echo the theme of our study, we decided to code our poster completely under \<svg\>  tags, which was presented on the Brown annual CS undergraduate research symposium.

<!--embed repo?-->

The poster has 3 backgrounds separated into 4 fields, and we showcased the flexibility of SVG images by including text play, gradient, textures, random dithering effect, and really the details of graphics you could achieve. During the symposium, we had both the printed version and live version of the poster to highlight SVG image's compactability. (Sadly, the quality of the poster was shrinked by the printer >_< ) However, we were still very proud to condense most of the creative uses of SVG in this poster.
You can find an animated version on [replit](https://replit.com/@Yuhanwww/SVG-Poster-Explore-CSR-Pearl-Zhang-and-Yuhan-Wang) :)

---
## Abstract
Nowadays, a minimalist white blank background is very common in web design to highlight information, adapt various screen sizes and reduce development cost. If not a white background, impressional solid color, gradient, or photo background are mostly used, which mostly appear in a raster image. However, with the help of \<svg\>  tag in html, we can create svg backgrounds with precise visual representations that are accessible, animatable, with the potential to be embedded in the web page without the need for additional loading. Pictures created in svg form are precise in vectors and will not lose quality in response to different sizes. With the help of inherent effects in \<svg\>  , we can apply textures, transformations, and animations that provide a wide range of visual effects. Pictures coded in \<svg\>  can be a new choice for web designers and can apply in many web applications like background or 3D scene, with the potential to bring back colorful unique web pages with different themes echoing the content.

If you want to take a closer look at the code or our logs, you are welcome to visit the [Github repo](https://github.com/yuhanwww/svg-creations)!