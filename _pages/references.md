---
layout: archive
author_profile: false
permalink: /reference/
---

{% include base_path %}
<!-- <h3 class="archive__subtitle">Examples from various domains</h3>		This destroys lists -->
{% assign items = site.posts | sort: 'title' %}
{% for post in items %}
{% if post.category == "reference" %}
  {% include archive-single-reference.html type="grid" %}      
{% endif %}
{% endfor %}

{% include paginator.html %}
