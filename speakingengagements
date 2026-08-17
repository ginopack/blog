---
layout: page
title: Speaking Engagements
permalink: /speaking/
---

## Upcoming Engagements

{% if site.data.speaking_upcoming.size > 0 %}
<ul>
{% for talk in site.data.speaking_upcoming %}
  <li>
    <strong>{{ talk.event }}</strong><br>
    {{ talk.session }}<br>
    <a href="{{ talk.url }}" target="_blank" rel="noopener">Event details &rarr;</a>
  </li>
  <br>
{% endfor %}
</ul>
{% else %}
<p>No upcoming engagements scheduled right now — check back soon.</p>
{% endif %}

---

## Past Engagements

{% assign past_sorted = site.data.speaking_past | sort: 'date' | reverse %}
{% if past_sorted.size > 0 %}
<ul>
{% for talk in past_sorted %}
  <li>
    <strong>{{ talk.event }}</strong>
    <span style="color: #828282;"> &mdash; {{ talk.date | date: "%b %-d, %Y" }}</span><br>
    {{ talk.session }}<br>
    <a href="{{ talk.media_url }}" target="_blank" rel="noopener">Download media &rarr;</a>
  </li>
  <br>
{% endfor %}
</ul>
{% else %}
<p>No past engagements listed yet.</p>
{% endif %}
