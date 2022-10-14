---
layout: page
title: Methodologies
permalink: /methodologies/
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

Note that the code included does not cover the whole procedure, various smaller actions are often left out for readability.

Other, much worse documented code can be found on
[Github](https://github.com/Kaspazas)
