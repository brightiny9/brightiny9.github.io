---
layout: default
title: 한국어
lang: ko
permalink: /ko/
---
<h1>글 목록</h1>
<p>작은 IT 회사를 굴리며 만들고, 실패하고, 배운 것을 솔직하게 적습니다.</p>
{% assign posts = site.posts | where: "lang", "ko" %}
<ul class="post-list">
{%- for post in posts %}
  <li><span class="post-meta">{{ post.date | date: "%Y-%m-%d" }}</span>
  <h3><a class="post-link" href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h3></li>
{%- endfor %}
</ul>
{% if posts.size == 0 %}<p>아직 글이 없습니다. 곧 첫 글이 올라옵니다.</p>{% endif %}
