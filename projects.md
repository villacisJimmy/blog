---
layout: default
title: My Projects
---

# My Projects 🚧

{% for project in site.projects %}
## [{{ project.title }}]({{ project.url | relative_url }})
{{ project.description }}

🔗 [Ver en GitHub]({{ project.link }})

---
{% endfor %}

[← Volver al inicio]({{ "/" | relative_url }})
