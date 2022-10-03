---
title: "Spring"
layout: single
permalink: /categories/spring
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Spring %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}