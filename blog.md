---
layout: default
title: Blog
---

# Blog 📝

Aquí están mis publicaciones:

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) ({{ post.date | date: "%B %d, %Y" }})
{% endfor %}
