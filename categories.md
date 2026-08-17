---
layout: page
title: Categories
permalink: /categories/
---

{% assign cats = site.categories | sort %}
{% for cat in cats %}

## {{ cat[0] }} <span style="font-weight: normal; color: #828282;">({{ cat[1] | size }})</span>

<ul>
{% for post in cat[1] %}
  <li>
    <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    <span style="color: #828282; font-size: 0.85em;"> &mdash; {{ post.date | date: "%b %-d, %Y" }}</span>
  </li>
{% endfor %}
</ul>

{% endfor %}
