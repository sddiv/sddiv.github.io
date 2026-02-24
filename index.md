---
layout: default
title: Home
---

{% if site.posts.size > 0 %}
<div class="posts-grid">
  {% for post in site.posts %}
    <article class="post-card">
      {% if post.featured_image %}
        <a href="{{ post.url | relative_url }}" class="post-card-image-link">
          <img src="{{ post.featured_image }}" alt="{{ post.title }}" class="post-card-image">
        </a>
      {% endif %}
      <div class="post-card-content">
        <span class="post-card-date">{{ post.date | date: "%b %d, %Y" }}</span>
        <h3 class="post-card-title">
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h3>
        {% if post.subtitle %}
          <p class="post-card-subtitle">{{ post.subtitle }}</p>
        {% endif %}
        {% if post.excerpt %}
          <p class="post-card-excerpt">{{ post.excerpt | strip_html | truncatewords: 35 }}</p>
        {% endif %}
        <div class="post-card-meta">
          {% assign words = post.content | number_of_words %}
          {% assign reading_time = words | divided_by: 200 %}
          {% if reading_time == 0 %}
            {% assign reading_time = 1 %}
          {% endif %}
          <span class="reading-time">{{ reading_time }} min read</span>
          {% if post.tags %}
            <div class="post-card-tags">
              {% for tag in post.tags limit:3 %}
                <span class="tag-badge">{{ tag }}</span>
              {% endfor %}
            </div>
          {% endif %}
        </div>
      </div>
    </article>
  {% endfor %}
</div>
{% else %}
  <p class="no-posts">No posts yet. Check back soon!</p>
{% endif %}
