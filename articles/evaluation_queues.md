---
title: Evaluation Queues
layout: article
excerpt: Evaluations queues are designed to support open-access data analysis and modeling challenges in Synapse. 
category: howto
---

# Evaluation Queues
Evaluations queues are designed to support open-access data analysis and modeling challenges in Synapse. This framework provides tools for administrators to collect and analyze data models from Synapse users created for a specific goal or purpose.

## Create an Evaluation Queue 

Synapse users can submit Synapse Files, or Synapse Docker containers to an Evaluation queue ("Evaluation" for short) which you manage.  You can create a new Evaluation using the R, Python or web client.  There are also ways to define submission 'rounds' (start date, round duration, and number of rounds) with optional submission quota (maximum submissions per participant or team) for each Evaluation queue.

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
							   numberOfRounds=1), #	The number of rounds, or null if there is no end. (Based on the duration of each round) ), #Sets the number of submissions allowed per participant/team
                  contentSource="syn12345", #Your synapse project id
                  submissionInstructionsMessage="Instructions on submission format...",
                  submissionReceiptMessage="Thanks for submitting to My Example Challenge!")
synStore(evaluation)
		{%endhighlight %}
	{% endtab %}

	{% tab Web %}
You can create evaluation queues on the web by navigating to your challenge site by adding /admin (E.g. www.synapse.org/#!Synapse:syn12345/admin).  Click **Tools** on the right corner and **Add Evaluation Queue** and follow the instructions on the screen.

<img src="/assets/images/create_evaluation_queues.png">

Unforuntately there is not a way to configure the round or quota settings of an evaluation queue from the web. Please view instructions in the R or Python tab for instructions on configuring the queues.
	{% endtab %}
{% endtabs %}


#### Share the Evaluation Queue with Participants

An Evaluation has a "contentSource" field which during creation should be set the Synapse ID of your challenge project.  Afterwards your project will have a "Challenge Admin" tab next to the Wiki and Files tabs.  Your new Evaluation(s) will appear in a list.  Click on an Evaluation will open a sharing tab.  The sharing levels are: Administer, "Can score", "Can Submit", and "Can view."  Give "Can Submit" to the Team or individuals who will be participating in the challenge.
"Administer" sharing should be tightly restricted, as it included authority to delete the entire Evaluation queue with all its contents.  The meaning of the other sharing levels is discussed below.
