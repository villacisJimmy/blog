---
layout: default
title: Blog
---

# Blog 📝

Lista de publicaciones:

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) ({{ post.date | date: "%B %d, %Y" }})
{% endfor %}
