---
layout: default
title: 한국어
lang: ko
permalink: /ko/
---
<div class="list-intro">
<h1 class="catalogue-title">글 목록</h1>
<p>작은 IT 회사를 굴리며 만들고, 실패하고, 배운 것을 솔직하게 적습니다.</p>
</div>
{% assign posts = site.posts | where: "lang", "ko" %}
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
{% if posts.size == 0 %}<p>아직 글이 없습니다. 곧 첫 글이 올라옵니다.</p>{% endif %}
