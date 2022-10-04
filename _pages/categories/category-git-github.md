---
title: "Git/Github"
layout: category-single
permalink: /categories/git-github
author_profile: true
category_nav: true
---
{% assign posts = site.categories.Git-Github %}
{% for post in posts %} {% include category-single.html type=page.entries_layout %} {% endfor %}