---
title: "Data Structure"
layout: category-single
permalink: /categories/data-structure
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Data-Structure %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}