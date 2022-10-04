---
title: "Tool"
layout: category-single
permalink: /categories/tool
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Tool %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}