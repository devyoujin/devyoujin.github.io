---
title: "Toy Project"
layout: category-single
permalink: /categories/toy-project
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Toy-Project %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}