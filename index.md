---
title: Blue Drumlin
---

Welcome to Blue Drumlin, a software company building with Ruby on Rails.

## Blue Drumlin builds
- A framework for e-commerce customer service - [SlopeCS](https://slopecs.com/)
- A location-based gardening journal - [GeoGardening](https://geogardening.app/)
- Better email validation & verification - Email200
- A project management tool for homeowners - DIY-er

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

X: [@BlueDrumlin](https://x.com/bluedrumlin)
