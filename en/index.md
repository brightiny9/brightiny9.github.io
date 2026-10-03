---
layout: default
title: English
lang: en
permalink: /en/
---
<h1>Posts</h1>
{% assign posts = site.posts | where: "lang", "en" %}
<ul class="post-list">
{%- for post in posts %}
  <li><span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
  <h3><a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h3></li>
{%- endfor %}
</ul>
{% if posts.size == 0 %}<p>No posts yet. The first one is coming soon.</p>{% endif %}
