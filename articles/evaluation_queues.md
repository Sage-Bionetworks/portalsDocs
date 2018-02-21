---
title: Evaluation Queues
layout: article
excerpt: Evaluations queues are designed to support open-access data analysis and modeling challenges in Synapse. 
category: howto
---

# Evaluation Queues
Evaluations queues are designed to support open-access data analysis and modeling challenges in Synapse. This framework provides tools for administrators to collect and analyze data models from Synapse users created for a specific goal or purpose.

## Create an Evaluation Queue 

Synapse users can submit Synapse Files, or Synapse Docker containers to an Evaluation queue ("Evaluation" for short) which you manage.  An Evaluation has a "contentSource" field which during creation should be set the Synapse ID of your challenge project.  Afterwards your project will have a **Challenge** tab next to the Wiki, Files and Tables tabs.  Your new Evaluation(s) will appear in a list.   You can create a new Evaluation using the R, Python or web client.  There are also ways to define submission 'rounds' (start date, round duration, and number of rounds) with optional submission quota (maximum submissions per participant or team) for each Evaluation queue. 

{% tabs %}
	{% tab Python %}
		{% highlight python %}
evaluation = Evaluation(name="My Example Challenge",
	description="Short description of challenge queue",
	status="OPEN",
	quota={'submissionLimit':3, #The maximum number of submissions per team/participant per round.
		'firstRoundStart':'2017-11-02T07:00:00.000Z', #The date/time at which the first round begins in UTC.
		'roundDurationMillis':1645199000, #The duration of each round.
		'numberOfRounds':1}, #	The number of rounds, or null if there is no end. (Based on the duration of each round) 
	contentSource="syn12345", #Your synapse project id
	submissionInstructionsMessage="Instructions on submission format...",
	submissionReceiptMessage="Thanks for submitting to My Example Challenge!")
syn.store(evaluation)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
evaluation <- Evaluation(name="My Example Challenge",
	description="Short description of challenge queue",
	status="OPEN",
	quota=synapseClient:::SubmissionQuota(submissionLimit=3, #The maximum number of submissions per team/participant per round.
		firstRoundStart = '2017-11-02T07:00:00.000Z', #The date/time at which the first round begins in UTC.
		roundDurationMillis = 1645199000, #The duration of each round.
		numberOfRounds=1), #	The number of rounds, or null if there is no end. (Based on the duration of each round)
	contentSource="syn12345", #Your synapse project id
	submissionInstructionsMessage="Instructions on submission format...",
	submissionReceiptMessage="Thanks for submitting to My Example Challenge!")
synStore(evaluation)
		{%endhighlight %}
	{% endtab %}

	{% tab Web %}
You can create evaluation queues on the web by navigating to your challenge site by adding `/admin` to the url (E.g. www.synapse.org/#!Synapse:syn12345/admin).  Click **Tools** on the right corner and **Add Evaluation Queue** and follow the instructions on the screen.

<img src="/assets/images/create_evaluation_queues.png">

	{% endtab %}
{% endtabs %}

## Configure an Evaluation Queue 

Unforuntately there is not a way to configure the round or quota settings of an evaluation queue from the web. The evaluation id can be found under the **Challenge** tab.  In the case below, the evaluation queue id is 9610091.  

<img style="width: 80%;" src="/assets/images/evaluation_queue_id.png">

Using this value, we can configure the `quota` parameters of this evaluation queue with the R or python client.  

{% tabs %}
	{% tab Python %}
		{% highlight python %}
evalId = 9610091
evaluation = syn.getEvaluation(evalId)
evaluation.quota = {'submissionLimit':3} #The maximum number of submissions per team/participant per round.
syn.store(evaluation)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
evalId = 9610091
evaluation <- synGetEvaluation(evalId)
evaluation$quota = synapseClient:::SubmissionQuota(firstRoundStart = '2017-11-02T07:00:00.000Z', #The date/time at which the first round begins in UTC.
	roundDurationMillis = 1645199000, #The duration of each round.
	numberOfRounds=1) #	The number of rounds, or null if there is no end. (Based on the duration of each round) 
synStore(evaluation)
		{%endhighlight %}
	{% endtab %}

{% endtabs %}


## Share an Evaluation Queue

Each Evaluation has its own sharing settings.  The sharing levels are: "Administrator", "Can score", "Can Submit", and "Can view."  
- "Administrator" sharing should be tightly restricted, as it includes authority to delete the entire Evaluation queue with all its contents. These users also have the ability to download all the submissions.
- "Can score" allows for individuals to download all the submissions
- "Can submit" allows for Teams or individuals to submit to the Evaluation, but doesn't have access to any of the submissions.
- "Can view" allows for Teams or individuals to view the submissions on a leaderboard.

To set the sharing setting, go to the **Challenge** tab and see your list of Evaluations.  Click on the `Share` button per Evaluation and share it with the Teams or individuals you would like.


## View Submissions of an Evaluation Queue
All submissions of an evaluation queue can be views through the use of leaderboard widgets in Wiki pages.  To learn how to create a wiki page, please visit [here](http://docs.synapse.org/articles/wikis.html).  Below are instructions on how to set up a leaderboard. You must know the evaluation id to do so.

<img style="width: 80%;" src="/assets/images/add_leaderboard_widget.png">

Once you click on **Leaderboard**, the below screen will pop up without any values.  You will have to input your own query statement such as `select * from evaluation_9610091`.  To view all the columns available, click **Refresh Columns**.
<img style="width: 80%;" src="/assets/images/configure_leaderboard_widget.png">

Clicking **Refresh Columns** will add these default columns.
<img style="width: 80%;" src="/assets/images/leaderboard_columns.png">


If you are happy with your leaderboard configurations, save both the configurations and the wiki page and you will see something like this. 
<img style="width: 80%;" src="/assets/images/leaderboard_on_wiki.png">




