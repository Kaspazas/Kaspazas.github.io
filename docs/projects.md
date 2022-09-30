---
layout: page
title: Projects
permalink: /projects/
---
Throughout my time studying, I authored several projects which I would like to highlight:

<ul>
 {% for work in site.works %}
   <h3>
     <a href="{{ work.url }}">
       {{ work.name }}
     </a>
   </h3>
   <p>{{ work.desc | markdownify }}</p>
 {% endfor %}
</ul>

Other, much worse documented code can be found at:
[github](https://github.com/Kaspazas)
