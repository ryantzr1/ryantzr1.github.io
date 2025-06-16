---
layout: default
title: Posts
permalink: /posts/
---

<div class="posts-container">
  <h1>All Posts</h1>
  
  <div class="twitter-link-section">
    <p>P.S. Right now, all my LLM-related posts are on <a href="{{ site.social_links[1].user_url }}" target="_blank" rel="noopener">Twitter</a>.</p>
  </div>
  
  <div class="posts-list">
    {% for post in site.posts %}
    <div class="post-item">
      <div class="post-title-section">
        <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
      </div>
      <span class="post-date">{{ post.date | date: "%B %d, %Y" }}</span>
    </div>
    {% endfor %}
  </div>
</div>
