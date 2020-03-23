---
title: Articles Index
layout: index
description: All documentation articles about Synapse.
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

<h3>Onboarding</h3>
<p>Get a brief overview of some of the main components of Synapse.</p>

<ul>
<li><b><a href="getting_started.html">Getting Started with Synapse</a></b>: A getting started guide for new users who are interested in learning about Synapse.</li>
<li><b><a href="user_profiles.html">User Accounts</a></b>: Create your user account and manage your profile.</li>
<li><b><a href="governance.html">Governance Overview</a></b>: A look at the Synapse governance process.</li>
<li><b><a href="accounts_certified_users_and_profile_validation.html">User Types including Certified Users</a></b>: Find out about the three levels of Synapse users and the privileges and responsibilities associated with each level.</li>
<li><b><a href="making_a_project.html">Making a Project</a></b>: An overview of Synapse Projects.</li>
<li><b><a href="discussion.html">Discussion Forums</a></b>: Explore the features of the discussion forum and how to use it to help your collaborations.</li>
<li><b><a href="wikis.html">Wikis</a></b>: Create wikis to provide narrative content for your research.</li>
<li><b><a href="getting_started_clients.html">Getting Started with the Synapse API Clients</a></b>: Use Synapse programmatically.</li>
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
