---
title: Challenge
layout: article
excerpt: Explores all aspects of DREAM challenges
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


## Challenge technical support

**More Information Coming Soon**

## Setting up a DREAM challenge infrastructure

This guide is meant to help challenge organizers create a space within Synapse to host the challenge, giving participants a place to learn about the challenge, join the challenge community, submit entries, track progress and view results.

### Creating Teams

In Synapse, Teams are publicly viewable groups of users.  Teams may be given access to projects, data files, and Evaluation submission queues as a group.  Using a Team for a challenge allows you to see who is participating and to conveniently control access to challenge resources.  **All challenges require a challenge participant, challenge pre-registrant, and administrator team.**

From the Synapse home page [https://www.synapse.org] enter a unique Team name to the left of the "Create Team" button, then click the button to create a new Team.  On the page for your Team you can configure whether approval is required by a Team administrator (you) to join the Team.  On this page you can also share administrative rights with other team members of your choice.

Please visit this [page]((http://docs.synapse.org/articles/teams.html) to learn more about teams.


### Creating DREAM Challenge Projects

Each Project, Folder and File may have an associated wiki page describing it.  The project wiki is a good place for an overview of the challenge and instructions for participating.  For background on how to create and share Projects, Files and Folders, please see our [making a project guide](http://docs.synapse.org/articles/making_a_project.html).  

All DREAM challenges should have a live and staging site.  The two projects should be named something like this:  "Your DREAM challenge" and "Your DREAM challenge staging site".  It is important to note that the live site will act as a splash site as the DREAM challenge is in development.  The main challenge project can serve as a 'landing page' for visitors wishing to learn about the challenge, as well as a repository for data files and other resources related to the challenge.  **All edits and changes even after the challenge has launched should be made on the staging site**

The comprehensive [DREAM Challenge Wiki Template](https://www.synapse.org/#!Synapse:syn2769515/wiki/) is a great starting point for your challenge's wiki pages.  It also helps to have a look at [some examples from previous challenges](https://www.synapse.org/#!Challenges:DREAM).  **This page will act as the staging site until the challenge is ready to be launched.  Then all the pages on the staging site will be copied onto the main site.** To copy the Challenge Wiki Template to your new project:  Say your private project is "syn0123456".   First, ensure your project has no wiki page (deleting the current one if necessary).  Here are the ways to copy a wiki from one project to another.

{% tabs %}
	{% tab Python %}
		{% highlight python %}
import synapseclient
import synapseutils
syn = synapseclient.login()
source_project_id = "syn2769515" # This is the ID of the template project
target_project_id = "syn0123456"
synapseutils.copyWiki(syn, source_project_id, target_project_id)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
library(synapseClient)
library(RCurl)
synapseLogin()
sourceProjectId<-"syn2769515" # This is the ID of the template project
targetProjectId<-"syn01234"
x<-getURL("https://gist.github.com/brucehoff/8f5e8975270e3b5d73f9/raw/2a4ac735d7992261bd6c3fdb519940cfbe08fbff/copyWikis.R", .opts=list(followlocation=TRUE))
source(textConnection(x))
copyWikis(sourceProjectId, targetProjectId)
#NOTE:  R Synapse client version 1.6-0 or later is required to correct a problem copying non-ASCII characters.
		{%endhighlight %}
	{% endtab %}

	{% tab Web %}
This script only works for apple computers. Download this [file](https://sourceforge.net/projects/createsynapsechallengewiki/files/createChallengeWiki.command/download) and double click the script.  You may have to right click and click open if you have script security settings on your computer. This script will prompt you to login to synapse.  Give it your private project syn0123456, and it will copy the template over. 
	{% endtab %}

{% endtabs %}



### Share the Project

Data access may be controlled at the Project, Folder or File level by clicking on the "Share" button in the upper right of any page, and selecting individual users or Teams and their access level.  A common pattern is to make the challenge project publicly viewable so all Synapse users can read about the challenge.  Participant data sets are organized in the project, but are limited in access so only challenge participants may see them.  Data used for testing/scoring submissions may
also be placed with the project but with even tighter access restrictions, so that only challenge organizers may see the data files.  

### Connect the Sign-up Team to the Challenge Project 

The API to call is [http://hud.rel.rest.doc.sagebase.org.s3-website-us-east-1.amazonaws.com/POST/challenge.html]. This registers the challenge team to the challenge site and creates a challenge Id.


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
library(synapseClient)
synapseLogin()
projectId<-"syn123456" # replace with the actual project Synapse ID
participantTeamId<-"987654" # replace with the actual Team ID
challenge<-list(projectId=projectId, participantTeamId=participantTeamId)
challenge<-synRestPOST("/challenge", challenge)
# retain the challenge ID (distinct from 'projectId', above) for use in several wiki widgets described below)
challengeId<-challenge$id
		{%endhighlight %}
	{% endtab %}
{% endtabs %}



Make sure to replace all the places that have `challengeId` in the staging site (3.2 - Forming a team)


### Configure Team Registration widgets

The challenge wiki template has placeholders for widgets which (1) register teams with the challenge, (2) list registered teams, and (3) list participants who have not joined any registered team.  At the time of this writing the templates appear in Sect. "3.2 - Forming a Team".  Edit the markdown to see the widget definitions:
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
projectId<-"syn123456" # replace with the actual challenge project ID
challenge<-synRestGET(sprintf("/entity/%s/challenge", projectId))
challenge$id
		{%endhighlight %}
	{% endtab %}
{% endtabs %}


### Add a Sign-up button

You can add a "Join" button on a wiki page to allow people to join your challenge.  Edit a wiki page, and click Insert > "Join Team Button".  A 'widget' will be added to your wiki page like this:
```
${jointeam?teamId=42&showProfileForm=true&isMemberMessage=You have successfully registered for the challenge&
text=Register for the Challenge&successMessage=Registration Request Accepted&
requestOpenText=Registration Request Accepted&isSimpleRequestButton=true&isChallenge=true}
```
You fill in the challenge Team ID and other parameters.  You can configure challenge registration to require that registrants agree to 'terms of use' (ToU) before they are allowed to join the challenge.   Further, mutiple terms can be associated with a single team.  For example, it is common to have participants agree both to the DREAM rules and also to terms that are specific to the particular challenge.  Adding these terms is the function of the Synapse Access and Compliance Team.  Please
contact them (act@sagebase.org), providing the text of the the ToU and the name and/or ID of the team.

### Edit Challenge Wiki Privately

**More information soon about the merge wiki script**
Challenge organizers have found it convenient to author wiki pages privately, then publish the result when ready for public view.  To do this, create a second project which you do _not_ share with the public, but only with fellow challenge organizers.  When complete, the content can be published using a script which is available in R or Python.  There are instructions above on how to copy wikis from one project to another. 


### Upload Challenge Data

As mentioned earlier, Synapse can serve both as a place for challenge administrators to share 'secret' scoring data files and for challenge participants to access training data used in the challenge.  You may share training data with participants by sharing with the challenge Team you created.

#### Add access restrictions

Synapse has the ability to apply access restrictions to sensitive, human data, so that legal requirements are met before participants access such data.  If human are being used in the challenge, or if you have any question about sensitivity of the challenge data, you must contact the Synapse Access and Compliance Team (act@sagebase.org) who will help put in place the necessary data access approval procedure.  

There are cases in which there are no human data concerns but for which a pop-up agreement needs to be presented before download data for the first time.  Contact the Access and Compliance Team to set up this agreement. 

### Create an Evaluation Queue for Submissions

Challenge participants submit their entries as Synapse Files to an Evaluation queue ("Evaluation" for short) which you manage.  You can create a new Evaluation using our R or Python client.  You may create multiple Evaluation queues to support sub-challenges having different types of submissions.  You may also define submission 'rounds' (start date, round duration, and number of rounds) with optional submission quota (maximum submissions per participant or team) for each Evaluation queue.

{% tabs %}
	{% tab Python %}
		{% highlight python %}
evaluation = Evaluation(name="My Example Challenge",
	  					description="Short description of challenge queue",
					    status="OPEN",
					    quota={'submissionLimit':3}, #Sets the number of submissions allowed per participant/team
					    contentSource="syn7824172", #Your synapse project id
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
                  quota=synapseClient:::SubmissionQuota(submissionLimit=3), #Sets the number of submissions allowed per participant/team
                  contentSource="syn7824172", #Your synapse project id
                  submissionInstructionsMessage="Instructions on submission format...",
                  submissionReceiptMessage="Thanks for submitting to My Example Challenge!")
synStore(evaluation)
		{%endhighlight %}
	{% endtab %}
{% endtabs %}




#### Share the Evaluation Queue with Participants

An Evaluation has a "contentSource" field which during creation should be set the Synapse ID of your challenge project.  Afterwards your project will have a "Challenge Admin" tab next to the Wiki and Files tabs.  Your new Evaluation(s) will appear in a list.  Click on an Evaluation will open a sharing tab.  The sharing levels are: Administer, "Can score", "Can Submit", and "Can view."  Give "Can Submit" to the Team or individuals who will be participating in the challenge.
"Administer" sharing should be tightly restricted, as it included authority to delete the entire Evaluation queue with all its contents.  The meaning of the other sharing levels is discussed below.

#### Enable Challenge Statistics

Share your Evaluations with the service account 'evaluationstatistics', giving 'Can Score' access.  This will result in a statistical summary of your challenge appearing on the page: [https://www.synapse.org/#!Synapse:syn2504723].

One way to enable statistics is with the following lines of Python:

```
evaluation = syn.getEvaluation(3317421)
syn.setPermissions(evaluation, principalId=0000001, accessType=['READ_PRIVATE_SUBMISSION', 'READ', 'UPDATE_SUBMISSION'])
```

#### Add a Submit button to your wiki

You can add a "Submit" button on a wiki page to allow people to submit entries to the Evaluation you set up.  Edit a wiki page, and click Insert > "Submit to Evaluation Button".  A 'widget' will be added to your wiki page like this:

```
${evalsubmit?subchallengeIdList=evalId1,evalId2&unavailableMessage=Join the team to submit to the challenge}
```

You customize the subchallengeIdList and other parameters.  The IDs in the subchallengeIdList are those shown in the Challenge Admin project tab. 

#### Large email volumes

Synapse has a limit on the volume of email messages sent out.  Currently accounts may not send more than ten messages per minute.  If you feel your scoring application needs to send larger volumes, please contact Synapse administration.

### Create a Scoring Application

As submissions arrive from participants, you may need to run a custom scoring script.  Synapse provides APIs for retrieving and scoring submissions.  A runnable scoring template (versions in Java, R and Python) is available in this Github repository:
[https://github.com/Sage-Bionetworks/SynapseChallengeTemplates]
After customizing the application for your scoring needs, create a periodically running job on a server owned by your organization.  A convenient, free web interface for periodically running jobs is Jenkins, [http://jenkins-ci.org/].  Note:  In the Challenge Admin tab mentioned above you must share the Evaluation with the user under whose credentials the Scoring Application is run, providing "Can score" access to this user.

Submission scores and other computational results may be attached to the Submissions themselves.  The sample code shows how to do this.  The results may be retrieved and displayed in a leader board, as described below.


#### Setting up a python scoring application

```
git clone https://github.com/Sage-Bionetworks/SynapseChallengeTemplates.git
```
**More Information Coming Soon**

#### Share Scoring Code with Participants

Although validation/test data is typically kept secret during a challenge, you should make the scoring algorithm itself available to participants.  A straightforward way to do this is to push the code to your Github fork, then link to a Synapse entity or wiki using its Github URL.

#### Create a Leader Board

You can add a dynamic leader board on a wiki page to show the submissions to an Evaluation and their scores.  Click "@" in the lower, right-hand corner of the portal, edit a wiki page, and click Insert > "Synapse API SuperTable".  A table editor allows you to pick from the results your scoring application added to the participants' submissions and display in a sorted, paginated, tabular form.  The scoring application templates mentioned above print out valid sample widget text suitable
for pasting into the wiki editor.  In the "Challenge Admin" control, described above, you provide "Can View" access to whoever you wish to be able to see the leader board, a choice which can be to make the leader board visible to everyone.

### Test everything on some dry run users

**DON'T SKIP THIS STEP!!!**  Really.  Get some friends to try to go through the whole process of signing up and submitting to the challenge, starting with just a link to synapse.org.  Do this 2 weeks before you intend to launch publicly so you can actually do the little bug fixing needed to smooth things out for the larger launch.

### Link results to participants' project spaces

If using a "live leader board", simply add a column whose value is "entityId".  This will add a column to the table containing hyperlinks to the submitter's home project.  There they can add a wiki describing their algorithm.  If using a static leader board (wiki table), you may retrieve the entity IDs from the submissions and add them in the wiki editor.  To get the link for each submission, you may use this R script:

```
library(synapseClient)
synapseLogin()
# give a list of submission IDs, for example
sids<-c(
"2703876",
"2700048",
"2700357",
"2700006",
"2701077",
"2699014")
# Now find the parent entity ID for each submitted file.
# Usually this will be the project containing the write-up.
# If not, it's just one click to go from the folder to the wiki.
# If the submitted file is erased, just link to the user himself.
for (sid in sids) {
        subm<-synGetSubmission(sid, downloadFile=F)
            reference<-sprintf("https://www.synapse.org/#!Profile:%s", subm$userId)
                try({
                            file<-synGet(subm"ntityId, downloadFile=F)
                        reference<-propertyValue(file, "parentId")
                            })
                    cat(subm$id, "\t", reference, "\n")
}
```