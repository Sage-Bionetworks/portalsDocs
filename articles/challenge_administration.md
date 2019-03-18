---
title: Challenge Infrastructure
layout: article
excerpt: Learn how to set-up the wireframe of a challenge. 
category: howto
---

## Challenge Guide Overview

This guide is meant to help organizers create a **challenge space** within Synapse to host a crowd-sourced challenge.  This space gives participants a place to learn about the challenge, join the challenge community, submit entries, track their progress and view results.  This document will focus on:

* Creation of the challenge space
* Configuration of the challenge space
* Scoring of the submitted entries


## Create a Challenge Space

Steps A1-5 below will be completed for you by using the `createchallenge` command after installing the [challengeutils](https://github.com/Sage-Bionetworks/challengeutils) python package.  This documentation below serves to provide detailed descriptions for each of the steps.

**For all DREAM challenges, please contact the Synapse Access and Compliance Team (act@sagebase.org) for step A4!**

### 1 - Challenge Projects

The command `createchallenge` creates two Synapse projects:
- **Live challenge project.** The 'live' challenge project can serve as a 'landing page' for visitors wishing to learn about the challenge, as well as a repository for data files and other resources related to the challenge.
- **Staging challenge project.** This project is used by the organizers during the development of the challenge to share files and draft the challenge wiki.

The command `createchallenge` requires you to provide a unique name for the challenge. If you specify "My Awesome Challenge", the Synapse projects "My Awesome Challenge" (live project) and "My Awesome Challenge - staging" will be created.

The wiki of the staging challenge project will be initialize with the [DREAM Challenge Wiki Template](https://www.synapse.org/#!Synapse:syn18058986/wiki/). Before editing it with content relevant to your challenge, please have a look at [some examples from past challenges](http://dreamchallenges.org/).

For background on how to create and share Projects, Files, Folders and wiki pages, please see our article [Making a Project](/articles/making_a_project.html).  

{% include important.html content="All edits and changes even after the challenge has launched should be made on the staging site." %}


### 2 - Synapse Teams

Here are the Synapse Teams created by the tool `createchallenge`:

* **Challenge Participant Team** - Synapse Projects must have a participant team associated with them for them to be a challenge.  This will allow users to register for your challenge.

* **Challenge Administrator Team** - This team is highly recommended to help assist in administrator access to challenge resources.

* **Challenge Pre-registration Team** - This team is recommended for when the challenge is under development.  It allows participants to join a mailing list to receive notification of challenge launch news.

Please visit this [page](/articles/teams.html) to learn more about teams. All three of these teams are created by using [challengeutils](https://github.com/Sage-Bionetworks/challengeutils).


### 3 - Connecting Participant Team to Challenge Project 

The participant team you created needs to be connected to the to the challenge to allow for participants to register for the challenge.

{% tabs %}
       {% tab Python %}
               {% highlight python %}
import synapseclient
import json
syn = synapseclient.login()
challenge_object = {'id': u'1000',
       'participantTeamId': u'1111', #replace with the actual Team ID
       'projectId': u'syn12345'} #replace with the MAIN project Synapse ID (not staging)
challenge = syn.restPOST('/challenge', json.dumps(challenge_object))
# retain the challenge ID (distinct from 'projectId', above) for use in several wiki widgets described below)
challenge_id = challenge['id']
#You will be able to access the challenge Id by doing
challenge = syn.restGET('/entity/syn12345/challenge')
challenge.id
               {% endhighlight %}
       {% endtab %}

       {% tab R %}
               {% highlight r %}
library(rjson)
library(synapser)
synLogin()
projectId <- "syn123456" # replace with the actual project Synapse ID
participantTeamId <- "987654" # replace with the actual Team ID
challenge <- list(projectId=projectId, participantTeamId=participantTeamId)
challenge <- synRestPOST("/challenge", toJSON(challenge))
# retain the challenge ID (distinct from 'projectId', above) for use in several wiki widgets described below)
challengeId<-challenge$id
               {%endhighlight %}
       {% endtab %}
	{% tab Web %}

Navigate to your challenge site and add `/challenge` to the end of the URL (E.g. www.synapse.org/#!Synapse:syn12345/challenge).  Click on `Challenge Tools`, `Run Challenge` and insert your challenge team name.

<img src="/assets/images/attachTeamToChallenge.png">


	{% endtab %}
{% endtabs %}

### 4 - Adding a Sign-up button

You can add a "Join" button on a wiki page to allow people to join your challenge.  Edit a wiki page, and click Insert > "Join Team Button".  A 'widget' will be added to your wiki page like this:

```
${jointeam?teamId=42&showProfileForm=true&isMemberMessage=You have successfully registered for the challenge&
text=Register for the Challenge&successMessage=Registration Request Accepted&
requestOpenText=Registration Request Accepted&isSimpleRequestButton=true&isChallenge=true}
```

You will have to fill in the challenge Team ID and other parameters.  You can configure challenge registration to require that registrants agree to 'terms of use' (ToU) before they are allowed to join the challenge.   Further, mutiple terms of use can be associated with a single team.  For example, it is common to have participants agree both to challenge rules and also to terms that are specific to the particular challenge.  Adding these terms is the function of the Synapse Access and Compliance Team.  Please
contact them (act@sagebase.org) and provide the text of the the ToU and the name and/or ID of the team.

{% include note.html content="Please contact the Synapse Access and Compliance Team with the Terms of Use and ID of your team prior to launching the challenge." %}

### 5 - Team Registration widgets

The challenge wiki template has placeholders for widgets which (1) register teams with the challenge, (2) list registered teams, and (3) list participants who have not joined any registered team.  At the time of this writing the templates appear in Sect. "How to participate" and "Participants & Teams".  Edit the markdown to see the widget definitions:

```
Register a Team for the challenge:
${registerChallengeTeam?challengeId=1234&buttonText=Register a Team} 

List the registered Teams:
${challengeTeams?challengeId=1234}

List registered participants who have not joined a registered Team:
${challengeParticipants?challengeId=1234&isInTeam=false}
```

In the template the challenge ID is the placeholder '1234'.  Replace this with the challenge ID for your challenge.  This ID was retained in the Python/R script in the section 'Connect the Sign-up Team to the Challenge Project', above.  If you did not retain this ID, you may look it up from the Challenge project ID.


{% tabs %}
	{% tab Python %}
		{% highlight python %}
challenge = syn.restGET("/entity/%s/challenge" % project_id) # project_id is defined above
challenge['id']
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
projectId <- "syn123456" # replace with the actual challenge project ID
challenge <- synRestGET(sprintf("/entity/%s/challenge", projectId))
challenge$id
		{%endhighlight %}
	{% endtab %}
	{% tab Web %}

Click on the Challenge Tab:

<img src="/assets/images/challengeId.png">


	{% endtab %}
{% endtabs %}


## B - Challenge Space Configuration

### 1 - Edit Challenge Wiki Privately

Challenge organizers have found it convenient to author wiki pages privately, then publish the result when ready for public view.  Please review [step A1](/articles/1---creating-challenge-projects).

If significant modifications to the public wiki are required, you can first edit the staging project wiki to test your edits. Once you are satisfied with your wiki edits, you can use the `mirrorwiki` command provided by [challengeutils](https://github.com/Sage-Bionetworks/challengeutils) to mirror the staging site changes to the live site so that only changes are made on the staging site.

{% include note.html content="The wiki titles are matched between the staging and live site, so if you don't want a page to be mirrored over, change the name of the wikipage." %}


### 2 - Upload Challenge Data

Synapse can serve both as a place for challenge administrators to share 'secret' scoring data files and for challenge participants to access training data used in the challenge.  You may share training data with participants by sharing with the challenge Team you created.  

#### 2.1 - Add access restrictions

Please view the [Sharing Settings and Conditions for Use](/articles/access_controls.html) to learn how to add access restrictions to the data.

Synapse has the ability to apply access restrictions to sensitive, human data, so that legal requirements are met before participants access such data.  If human are being used in the challenge, or if you have any question about sensitivity of the challenge data, you must contact the Synapse Access and Compliance Team (act@sagebase.org) who will help put in place the necessary data access approval procedure.  

There are cases in which there are no human data concerns but for which a pop-up agreement needs to be presented before download data for the first time.  Contact the Access and Compliance Team to set up this agreement. 

### 3 - Create an Evaluation Queue for Submissions

Challenge participants submit their entries as Synapse Files to an Evaluation queue ("Evaluation" for short) which you manage.  You may create multiple Evaluation queues to support sub-challenges having different types and rounds of submissions.

Please visit the [Evaluation Queue article](/articles/evaluation_queues.html) to learn about queues.

### 4 - Share the Challenge!

Now that you have successfully configured the challenge. Please view the [Access Controls article](/articles/access_controls.html) to learn how to share the challenge and apply conditions for use on the data.

A common pattern is to make the challenge project publicly viewable so all Synapse users can read about the challenge.  Participant data sets are organized in the project, but are limited in access so only challenge participants may see them.  Data used for testing/scoring submissions may also be placed with the project but with even tighter access restrictions, so that only challenge organizers may see the data files. 


## C - Scoring Submissions
Every submission has a unique submission id, this should not be confused with synapse ids which start with `syn`.  A submission can also contain annotations that can be used to display on live leaderboards.  It is good to note that these added annotations can be set to either public or private.  Private annotations cannot be read by people on the live leaderboard unless the READ_PRIVATE_SUBMISSIONS ACL is set on the evaluation queue.  Learn more about submissions in the [Evaluation Queue article](/articles/evaluation_queues.html)

{% tabs %}
	{% tab Python %}
		{% highlight python %}
#Get submission / annotations
sub = syn.getSubmission(submissionId)
annotations = syn.getSubmissionStatus(submissionId)
#Get all scored submissions in an evaluation queue
e = syn.getEvaluation(e)
bundles = syn.getSubmissionBundles(e, status = "SCORED")
for sub, status in bundles:
	#validate submission
	#score submission
	print(sub)
	print(status)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
# Get submission / annotations
sub <- synGetSubmission(submissionId)
annotations <- synGetSubmissionStatus(submissionId)
# Get all scored submissions in an evaluation queue
bundles <- as.list(synGetSubmissionBundles(evaluation, status="SCORED"))
		{%endhighlight %}
	{% endtab %}
{% endtabs %}


### 1 - Revealing Submissions and Scores

To reveal submissions of a challenge, organizers can create a leaderboard. Leaderboards are sorted, paginated, tabular forms that display submission annotations (such as scores from your scoring application and other metadata). Leaderboards are dynamic and update as annotations/scores change, so can provide real-time insight into how your Challenge is going. The scoring application templates mentioned above print out valid sample widget text suitable for pasting into the wiki editor.  In the "Challenge Admin" control, described above, you provide "Can View" access to whomever you wish to be able to see the leaderboard. 

To add a leaderboard to your Challenge Wiki,
* First go to the Challenge Project and get the ID of the Evaluation of interest; Challenges can have multiple evaluations so it's important to identify which evaluation you want to summarize.
* Next, edit the wiki page where you want to add your leaderboard and choose "Insert" and then "Leaderboard". 
* Finally, you'll configure your leaderboard by entering a query of the form "Select * from Evaluation_12345" where 12345 is the ID from the first step. 

<br>If you have some annotations already then you can click "Refresh Columns" to add display columns for the existing annotations. Otherwise you have to add the columns manually. You can reorder the columns and choose what to sort by. Keep in mind that "private" annotations will not be visible to participants (only to challenge administrators). 

