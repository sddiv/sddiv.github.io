---
layout: default
title: Archive
---

# Blog Archive

<div class="archive-container">
  {% assign postsByYear = site.posts | group_by_exp: "post", "post.date | date: '%Y'" %}
  {% for year in postsByYear %}
    <div class="archive-year">
      <h2>{{ year.name }}</h2>
      <div class="archive-posts">
        {% for post in year.items %}
          <article class="archive-post">
            <span class="archive-date">{{ post.date | date: "%b %d" }}</span>
            <div class="archive-post-info">
              <h3><a href="{{ post.url | relative_url }}">{{ post.title }}</a></h3>
              {% if post.tags %}
                <div class="archive-tags">
                  {% for tag in post.tags limit:3 %}
                    <span class="tag-badge">{{ tag }}</span>
                  {% endfor %}
                </div>
              {% endif %}
            </div>
          </article>
        {% endfor %}
      </div>
    </div>
  {% endfor %}
</div>

{% if site.posts.size == 0 %}
  <p class="no-posts">No posts yet.</p>
{% endif %}
