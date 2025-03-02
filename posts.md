---
layout: default
title: Posts
permalink: /posts/
---

<h1>All Posts</h1>

<ul class="post-list">
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h2>
      <span>{{ post.date | date: "%B %d, %Y" }}</span>
      <p>{{ post.description | default: post.excerpt }}</p>
    </li>
  {% endfor %}
</ul>