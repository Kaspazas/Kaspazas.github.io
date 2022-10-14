---
layout: page
title: Methodologies
permalink: /Methodologies/
---
In analyzing social media data, I've used a variety of methodologies, including, but not limited to:
<ul>
 {% for method in site.methods %}
   <h3>
     <a href="{{ method.url }}">
       {{ method.name }}
     </a>
   </h3>
   <p>{{ method.desc | markdownify }}</p>
 {% endfor %}
</ul>

Other, much worse documented code can be found on
[Github](https://github.com/Kaspazas)
