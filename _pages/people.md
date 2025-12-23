---
layout: archive
title: "People"
permalink: /people/
author_profile: true
redirect_from:
  - /people
---

{% include base_path %}

{% for post in site.team %}
  {% include archive-single.html type="grid" %}
{% endfor %}
