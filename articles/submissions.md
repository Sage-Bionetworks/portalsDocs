---
title: Submission
layout: article
excerpt: Explore the features of submissions made to evaluation queues
category: howto
---

<style>
#image {
    width: 50%;
}
</style>

# Submission

Every submission you make to an Evaluation queue has a unique submission id attached to it.  This id should not be confused with Synapse ids which start with syn...  All submissions have a Submission and SubmissionStatus object attached to it.  A submission can also contain annotations that can be used to display on live leaderboards.  It is good to note that these added annotations can be set to either public or private.  Private annotations cannot be read by people on the live leaderboard unless the READ_PRIVATE_SUBMISSIONS ACL is set on the evaluation queue.

{% tabs %}
	{% tab Python %}
		{% highlight python %}
import synapseclient
syn = synapseclient.login()
#Get submission / annotations
sub = syn.getSubmission(submissionId)
annotations = syn.getSubmissionStatus(submissionId)
#Get all scored submissions in an evaluation queue
e = syn.getEvaluation(e)
bundles = syn.getSubmissionBundles(e, status = "SCORED")
for sub, status in bundles:
	print(sub)
	print(status)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
# Get submission / annotations
library(synapseClient)
synapseLogin()
sub <- synGetSubmission(submissionId)
annotations <- synGetSubmissionStatus(submissionId)
# Get all scored submissions in an evaluation queue
bundles <- as.list(synGetSubmissionBundles(evaluation, status="SCORED"))
		{%endhighlight %}
	{% endtab %}
{% endtabs %}
