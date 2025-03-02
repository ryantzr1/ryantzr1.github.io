---
layout: page
title: Backend
permalink: /categories/backend/
---

<ul>
  {% for post in site.categories.backend %}
    <li><a href="{{ post.url }}">{{ post.title }}</a> ({{ post.date | date: "%b %-d, %Y" }})</li>
  {% endfor %}
</ul>