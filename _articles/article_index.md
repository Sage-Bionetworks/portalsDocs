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

<!--- The get started 'category' is only used for the card on the index page. --->
<!--- It should be skipped here. --->
{% unless category.name == "get-started" %}

<div class="tab-pane active" id="{{ category.name }}">

<h3>{{ category.title }}</h3>
<p>{{ category.excerpt }}</p>

{% for group in grouped_articles %}
{% if group.name contains category.name and group.items.size > 0 %}
{% assign pages = group.items | sort: "order" %}

<ul>

{% for page in pages %}
<li><b><a href="{{ page.url | relative_url}}">{{ page.title }}</a></b>: {{page.excerpt}}</li> {%endfor%}
</ul>

{% endif %}
{%endfor%}

</div>

<!-- TODO replace this with style -->
<br/>
<br/>

{% endunless %}
{% endfor %}

</div>

<div class="clearfix"></div>
