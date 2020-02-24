---
title: Articles Index
layout: index
description: All documentation articles about Synapse.
---

<div class="col-xs-12 col-md-12 col-lg-12" id="subjects">

{% assign categories = site.categories | sort: "order" %}
{% assign sections = site.sections | sort: "order" %}
{% assign grouped_articles = site.articles | group_by: "category" | sort: "order"  %}

{% for category in categories %}

<div class="tab-pane active" id="{{ category.name }}">

{% for group in grouped_articles %}
{% if group.name contains category.name and group.items.size > 0 %}
{% assign pages = group.items | sort: "order" %}
{% break %}
{% endif %}
{%endfor%}

<b>Size {{ pages.size }}</b>
<h3>{{ category.title }}</h3>
<p>{{ category.excerpt }}</p>

<ul>

{% for page in pages %}
<li><b><a href="{{ page.url | relative_url}}">{{ page.title }}</a></b>: {{page.excerpt}}</li>    {%endfor%}
</ul>
</div>

<!-- TODO replace this with style -->
<br/>
<br/>

{% endfor %}

</div>

<div class="clearfix"></div>
