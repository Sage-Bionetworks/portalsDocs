---
title: Submitting to a DREAM Challenge
layout: article
excerpt: Learn how to submit to a challenge
---

## Submitting to challenges

One major part of the challenge is ofcourse submitting to the challenge itself.  There are multiple ways a participant can submit to a challenge by using the R, python or web client.  Below is a quick tutorial on how to submit to a challenge.  Most challenge queues will be labeled by `challengename-subchallenge#` as a challenge may have different questions that it may want participants to answer.  

To submit to a challenge, one must have uploaded an entity first to their project and know the evaluation id of the subchallenge you are trying to submit to.  This number can be found in the challenge tab of the challenge site in parenthesis. 

<img src="/assets/images/evaluationQueue.png">

In these R and python examples, we will be uploading a file to an example project then submitting that file to the challenge. The submission function takes two optional parameters: name and team.  Name can be provided to serve as a custom name of the submission, if name isn't provided the name of the entity being submitted will be used as the name.  Team can optionally be provided to give credit to members of the team that contributed to the submission. The team must be registered for the challenge with which the given evaluation is associated. The caller must be a member of the submitting team.

{% tabs %}
	{% tab Python %}
		{% highlight python %}
import synapseclient
from synapseclient import File
syn = synapseclient.login()
mySubmission = File("/path/to/submission.csv",parent = "syn12345")
mySub = syn.store(mySubmission)
submission = syn.submit(evaluationId, mySub, name='Our Final Answer', team='Blue Team')
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
library(synapseClient)
mySubmission <- File("/path/to/submission.csv",parentId="syn12345")
mySub <- synStore(mySubmission)
submission <- submit(evaluation = "evaluationId", entity = mySub, submissionName='Our Final Answer', teamName='Blue Team') #The evaluationId HAS to be a string here or there will be an error
		{%endhighlight %}
	{% endtab %}

	{% tab Web %}
Navigate to an uploaded file in synapse and click on tools and click submit to challenge
<img src="/assets/images/howtosubmit.png">
After doing so, pick the challenge you want to submit to, in this case (My Example Challenge). Click Next and follow the steps to complete your submission.
<img src="/assets/images/submitToChallenge.png">
	{% endtab %}

{% endtabs %}
