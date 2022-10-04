---
title: "Spring"
layout: category-single
permalink: /categories/spring
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Spring %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}