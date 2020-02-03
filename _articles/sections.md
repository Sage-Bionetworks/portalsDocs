---
title: Sections
layout: index
---

<center><p>These are the main instructions for using Synapse on the web and through the programmatic clients. Pick an area that interests you, or read them in order, to improve your knowledge of Synapse. </p></center>

{% assign sections = site.sections | sort: "order" %}

{% assign grouped_categories = site.categories | group_by: "section" | sort: "order"  %}

{% for section in sections %}

<div class="tab-pane active" id="{{ section.name }}">

<h3>{{ section.title }}</h3>
<p>{{ section.excerpt }}</p>
</div>
<div class="col-xs-12 col-sm-12 col-lg-12" id="subjects">
    <ul class="nav nav-tabs" id="myTab" style="margin-top: -70px; border: 2px solid transparent;">

    {% for group in grouped_categories %} {% if group.name == section.name %}

    {% assign categories = group.items | sort: "order" %}

    {% for category in categories %}
    <div class="col-xs-12 col-sm-3">
        <a href="#{{ category.name }}">
        <div class="subject-card">
            <h5>{{ category.title }}</h5>
            <hr>
            <p>{{ category.explanation }}</p>
        </div>
        </a>
    </div>
    {% endfor %}
    {% endif %}{% endfor %}
    </ul>
</div>

<div class="clearfix">

{% endfor %}
