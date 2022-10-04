---
title: "Operating System"
layout: category-single
permalink: /categories/operating-system
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Operating-System %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}