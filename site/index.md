---
layout: default
permalink: /index.html
---

# Home Page

{% assign pages = site.pages | where_exp: 'page', 'page.title' %}
{% for page in pages %}
    title: {{page.title}}
{% endfor %}