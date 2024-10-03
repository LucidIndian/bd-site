---
title: Blue Drumlin
---

## Blue Drumlin builds
- A framework for e-commerce customer service - SlopeCS
- A location-based gardening journal - GeoGardening
- A project management tool for DIY homeowners - DIY-er

## Posts

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

X: @BlueDrumlin
