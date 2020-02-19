---
title: Articles Index
layout: index
description: All documentation articles about Synapse.
---

<div class="col-xs-12 col-md-12 col-lg-12" id="subjects">

{% assign categories = site.categories | sort: "order" %}
{% assign sections = site.sections | sort: "order" %}
{% assign groups = site.articles | group_by: "category" | sort: "order"  %}

{% for category in categories %}
<div class="tab-pane active" id="{{ category.name }}">

<h3>{{ category.title }}</h3>
<p>{{ category.excerpt }}</p>

{% for group in groups %} {% if group.name contains category.name %}
<ul>
{% assign pages = group.items | sort: "order" %}

{% for page in pages %}
<li><b><a href="{{ page.url | relative_url}}">{{ page.title }}</a></b>: {{page.excerpt}}</li>    {%endfor%}
</ul>
{% endif %} {%endfor%}
</div>
{% endfor %}

</div>

<div class="clearfix"></div>
