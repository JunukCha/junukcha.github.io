---
layout: default
title: Projects
permalink: /projects/
---

# Projects

{% for project in site.projects %}
  <div>
    <h3><a href="{{ project.url }}">{{ project.title }}</a></h3>
    <p>{{ project.content | strip_html | truncate: 160 }}</p>
  </div>
{% endfor %}
