---
title: "Java"
layout: category-single
permalink: /categories/java
author_profile: true
category_nav: true
---

{% assign posts = site.categories.Java %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}