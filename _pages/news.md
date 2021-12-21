---
layout: archive
title: "News"
permalink: /news/
author_profile: true
redirect_from:
  - /news
---

{% include base_path %}

{% for post in site.news %}
  {% include archive-single.html type="grid" %}
{% endfor %}
