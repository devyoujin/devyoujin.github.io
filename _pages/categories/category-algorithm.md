---
title: "Algorithm"
layout: single
permalink: /categories/algorithm
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Algorithm %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}