---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---

## Blue Drumlin builds
- A framework for e-commerce customer service - SlopeCS
- A location-based gardening journal - GeoGardening
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