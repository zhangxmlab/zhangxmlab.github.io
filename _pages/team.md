---
layout: archive
title: "Team"
permalink: /team/
author_profile: true
redirect_from:
  - /team
---

{% include base_path %}

{% for post in site.team %}
  {% include archive-single.html type="grid" %}
{% endfor %}
