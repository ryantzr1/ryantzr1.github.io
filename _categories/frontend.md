---
layout: page
title: Frontend
permalink: /categories/frontend/
---

<ul class="post-list">
  {% for post in site.posts %}
    {% if post.categories contains "frontend" %}
      <li>
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
        <span>{{ post.date | date: "%B %d, %Y" }}</span>
        <p>{{ post.excerpt | strip_html | truncatewords: 30 }}</p>
      </li>
    {% endif %}
  {% endfor %}
</ul>