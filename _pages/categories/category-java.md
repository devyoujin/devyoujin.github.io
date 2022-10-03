---
title: "Java"
layout: single
permalink: /categories/java
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Java %}
{% for post in posts %} {% include archive-single.html type=page.entries_layout %} {% endfor %}