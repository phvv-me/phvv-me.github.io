---
layout: default
permalink: /index.html
---

# Home Page

## Pages

<ul>
{% for page in site.pages %}
  <li><a href="{{ page.url }}">{{ page.title }}</a></li>
{% endfor %}
</ul>

