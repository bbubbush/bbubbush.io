---
layout: page
title: Posts
description: 
permalink: /posts/
---

<div class="posts">
    <h2>이곳은 포스트 리스트!</h2>
</div>

{% for post in site.posts %}

    <article class="post-preview">
    <a href="{{ post.url | prepend: site.baseurl | replace: '//', '/' }}">
        <h2 class="post-title">{{ post.title }}</h2>
        {% if post.subtitle %}
        <h3 class="post-subtitle">{{ post.subtitle }}</h3>
        {% else %}
        <h3 class="post-subtitle">{{ post.excerpt | strip_html | truncatewords: 15 }}</h3>
        {% endif %}
    </a>
    <p class="post-meta">Posted by
        {% if post.author %}
        {{ post.author }}
        {% else %}
        {{ site.author }}
        {% endif %}
        on
        {{ post.date | date: '%B %d, %Y' }}</p>
    </article>

    <hr>

{% endfor %}
