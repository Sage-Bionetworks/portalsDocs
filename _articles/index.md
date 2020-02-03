---
title: Articles
layout: index
---
<center> These are the main instructions for using Synapse on the web and through the programmatic clients. Pick an area that interests you, or read them in order, to improve your knowledge of Synapse. </center>

<!-- {% assign doclist = site.pages | sort: 'order' %} -->
{% assign categories = site.categories | sort: "order" %}

<div class="col-xs-12 col-sm-12 col-lg-12" id="subjects">
    <ul class="nav nav-tabs" id="myTab" style="margin-top: -70px; border: 2px solid transparent;">

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
    </ul>

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

    <div class="clearfix"></div>
</div>
