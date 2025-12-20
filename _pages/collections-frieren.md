---
title: "Frieren"
layout: archive
permalink: /collection/frieren/
taxonomy: frieren
author_profile: false
classes: wide
---

![Frieren]({{ site.baseurl }}/assets/images/themes/frieren.jpg)

Weiss Schwarz cards from the Frieren set.

{% assign collection_posts = site.categories.frieren %}
{% for post in collection_posts %}
  {% include archive-single.html %}
{% endfor %}
