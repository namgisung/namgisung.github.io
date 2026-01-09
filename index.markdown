---
layout: home
title: Home
---

## 📘 Wiki

{% assign wikis = site.pages | where: "wiki", true | sort: "order" %}

<ul>
{% for wiki in wikis %}
  <li>
    <a href="{{ wiki.url | relative_url }}">
      {{ wiki.title }}
    </a>
  </li>
{% endfor %}
</ul>
