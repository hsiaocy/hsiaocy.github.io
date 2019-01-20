---
layout: archive
title: "Latest Posts"
permalink: /notes/
---

<div class="tiles">
{% for post in site.categories.notes %}
	{% include post-grid.html %}
{% endfor %}
</div><!-- /.tiles -->
