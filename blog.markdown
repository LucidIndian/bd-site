---
layout: page
title: Blog
permalink: /blog/
---

## Posts about building with Ruby on Rails

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>