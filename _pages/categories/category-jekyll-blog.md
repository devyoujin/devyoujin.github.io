---
title: "Jekyll Blog"
layout: single
permalink: /categories/jekyll
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Jekyll-Blog %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}