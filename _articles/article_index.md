---
title: Articles
layout: index
description: An index of articles available about Sage Portals.
---

<div class="col-xs-12 col-md-12 col-lg-12" id="subjects">

{% assign categories = site.categories | sort: "order" %}
{% assign sections = site.sections | sort: "order" %}
{% assign grouped_articles = site.articles | group_by: "category" | sort: "order"  %}

<!-- Onboarding needs a specific ordering that is difficult to get with a loop.
	 Instead, we have to hardcode the ordering for the onboarding category.
	 Note that if the excerpt changes in the article, it will not reflect the
	 change on the index page. The excerpt must be updated here.
-->
<div class="tab-pane active" id="onboarding">

<h3>Starting a New Portal</h3>
<p>Get a brief overview of some of the main components of Synapse-powered portals.</p>

<ul>
<li><b><a href="getting_started.html">Getting Started with Sage Portals</a></b>: A getting started guide for users who are interested in learning about Synapse-powered community portals.</li>
</ul>
<br/>
<br/>
</div>

<!-- Create rest of categories that don't need to be manually hand-crafted. -->
{% for category in categories %}

<!--- The get started and onboarding 'categories' are only used for the card on the index page. --->
<!--- They should be skipped here. --->
{% unless category.name == "get-started" or category.name == "onboarding" %}

<div class="tab-pane active" id="{{ category.name }}">

<h3>{{ category.title }}</h3>
<p>{{ category.explanation }}</p>

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
