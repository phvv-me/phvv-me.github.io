---
layout: home
permalink: /index.html
---

# Home Page

## Pages

<!-- TODO: remove homepage from the list -->
{% assign pages = site.pages | where_exp: 'page', 'page.title' %}

<ul>
{% for page in pages %}
  <li><a href="{{ page.url }}">{{ page.title }}</a></li>
{% endfor %}
</ul>

