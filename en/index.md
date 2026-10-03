---
layout: default
title: English
lang: en
permalink: /en/
---
<div class="list-intro">
<h1 class="catalogue-title">Posts</h1>
<p>Running a tiny IT company: building, failing, and writing down what we learn, honestly.</p>
</div>
{% assign posts = site.posts | where: "lang", "en" %}
<div class="catalogue">
{%- for post in posts %}
  <a href="{{ post.url | relative_url }}" class="catalogue-item">
    <div>
      <time datetime="{{ post.date | date_to_xmlschema }}" class="catalogue-time">{{ post.date | date: "%Y-%m-%d" }}</time>
      <h1 class="catalogue-title">{{ post.title | escape }}</h1>
      <div class="catalogue-line"></div>
      <p>{{ post.content | strip_html | truncatewords: 30 }}</p>
    </div>
  </a>
{%- endfor %}
</div>
{% if posts.size == 0 %}<p>No posts yet. The first one is coming soon.</p>{% endif %}
