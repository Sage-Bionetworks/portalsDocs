---
title: Articles
layout: index
description: These are the main instructions for using Synapse. Pick an section that interests you or read them in order.
---

<div class="col-xs-12 col-md-12 col-lg-12" id="subjects">

<!-- {% assign doclist = site.pages | sort: 'order' %} -->
{% assign categories = site.categories | sort: "order" %}
{% assign sections = site.sections | sort: "order" %}
{% assign category_groups = site.categories | group_by: "section" | sort: "order"  %}

{% for section in sections %}

<!-- <div class="tab-pane active" id="{{ section.name }}"> -->

<!-- TODO: centering is being done via html tag, but should be css -->
<center><h3>{{ section.title }}</h3>
<p>{{ section.explanation }}</p></center>

{% for group in category_groups %} {% if group.name contains section.name %}
{% assign pages = group.items | sort: "order" %}

<div class="col-xs-12 col-md-12 col-lg-12 col-sm-12" id="subjects" style="background-color: transparent;">

{% for page in pages %}
<div class="col-xs-12 col-sm-4">
<a href="article_index.html#{{ page.name }}">
<div class="subject-card">
    <h5>{{ page.title }}</h5>
    <hr>
    <p>{{ page.excerpt }}</p>
</div>
</a>
</div>
{% endfor %}

</div>

{% endif %} {%endfor%}
<!-- </div> -->
{% endfor %}


</div>

<div class="clearfix"></div>
