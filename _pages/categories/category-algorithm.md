---
title: "Algorithm"
layout: category-single
permalink: /categories/algorithm
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Algorithm %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}