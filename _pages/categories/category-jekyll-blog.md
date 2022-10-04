---
title: "Jekyll Blog"
layout: category-single
permalink: /categories/jekyll-blog
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Jekyll-Blog %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}