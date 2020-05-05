---

title: Evaluation Queues
layout: article
excerpt: A Synapse Queue contains user submitted models or files to execute for challenges and benchmarking.
category: reproducible-research
---

An Evaluation queue allows for people to submit Synapse `Files`, `Docker` images, etc. for evaluation. They are designed to support open-access data analysis and modeling challenges in Synapse. This framework provides tools for administrators to collect and analyze data models from Synapse users created for a specific goal or purpose.

## Create an Evaluation Queue

To create a queue, you must first create a Synapse `Project` or have [edit permissions]({{ site.baseurl }}{% link _articles/sharing_settings.md %}#edit-permissions) on an existing Project. To create a Synapse Project, follow the instructions on the [Project and Data Management]({{ site.baseurl}}{% link _articles/getting_started.md %}#making-and-managing-projects-in-synapse) page. 

Once you've created your project, navigate to it and add `/challenge` to the url (e.g. www.synapse.org/#!Synapse:syn12345/challenge). Click **Tools** in the right corner and select **Add Evaluation Queue**.

<img style="width: 80%;" src="/assets/images/create_evaluation_queues.png">

An Evaluation queue can take several parameters that you can use to customize your preferences.

* Name – Unique name of the evaluation
* Description – A short description of the evaluation
* Submission Instructions – Message to display to users detailing acceptable formatting for submissions.
* Submission Receipt Message – Message to display to users upon submission

{% include note.html content="The name of your evaluation queue MUST be unique, otherwise the queue will not be created." %}


### Setting Quotas on an Evaluation Queue

Optionally, you can restrict how things are submitted by using a quota.

<img style="width: 40%;" src="/assets/images/evaluation_queue_quota.png">


An Evaluation queue can only have one quota. You may specify the length of time the queue is open, the start date, round duration, and number of rounds. These are required parameters. It is optional to set submission limit.

* First Round Start Date/Time - The date/time at which the first round begins.
* Number of Rounds - The number of rounds, or null if there is no limit to set.
* Submission Limit - The maximum number of submissions per team/participant per round. Please keep in mind that the system will prevent additional submissions by a user/team once they have hit this number of submissions.
* Round Duration  - The duration of each round. If you set a round duration you will want to set the number of rounds or it will assume an infinite number of rounds.


## Share an Evaluation Queue

Each Evaluation has sharing settings, which limit who can interact with the Evaluation.

* **Administrator** sharing should be tightly restricted, as it includes authority to delete the entire Evaluation queue and its contents. These users also have the ability to download all of the submissions.
* **Can Score** allows for individuals to download all of the submissions
* **Can Submit** allows for teams or individuals to submit to the Evaluation, but doesn't have access to any of the submissions.
* **Can View** allows for teams or individuals to view the submissions on a leaderboard.

To set the sharing settings, go to the **Challenge** tab to view your list of Evaluations.  Click on the **Share** button per Evaluation and share it with the teams or individuals you would like.

{% include important.html content="When someone submits to an Evaluation, a copy of the submission is made, so a person with Administrator or Can score access will be able to download the submission even if the submitter deletes the entity." %}

## Close an Evaluation Queue
While there isn't technically a way of "closing" an evaluation queue, there are multiple ways to discontinue submissions for users.

* Users are only able to submit to a queue if they have `can submit` permissions to it. If you have the ability to modify the permissions of a queue, you will still be able to submit to the queue due to your `administrator` access.
* If the quota is set so the current date exceeds the the round start + round duration, no one will be able to submit to the queue. This includes users with administrator permissions.
* Deleting a queue will also discontinue the ability to submit to it. Be careful when doing this, as deleting a queue is irreversible - you will lose all its submissions.


## Submitting to an Evaluation Queue

Any Synapse entity may be submitted to an Evaluation Queue.

In the R and Python examples, you need to know the ID of the evaluation queue. This ID must be provided to you by administrators of the queue. 

The submission function takes **two optional parameters**: `name` and `team`.  Name can be provided to customize the submission. The submission name is often used by participants to identify their submissions.  If a name is not provided, the name of the entity being submitted will be used. As an example, if you submit a File named testfile.txt, and the name of the submission isn't specified, it will default to testfile.txt. Team names can be provided to recognize a group of contributors.

##### Python

```python
import synapseclient

syn = synapseclient.login()

evaluation_id = "9610091"
my_submission_entity = "syn1234567"

submission = syn.submit(
    evaluation = evaluation_id,
    entity = my_submission_entity,
    name = "My Submission", # An arbitrary name for your submission
    team = "My Team Name") # Optional, can also pass a Team object or id
```

##### R

```r
library(synapser)

synLogin()

evaluation_id <- "9610091"
my_submission_entity <- "syn1234567"

submission <- synSubmit(
    evaluation = evaluation_id,
    entity = my_submission_entity,
    name = "My Submission", # An arbitrary name for your submission
    team = "My Team Name") # Optional, can also pass a Team object or id
```
## Submissions

Every submission you make to an Evaluation queue has a unique ID. This ID should not be confused with Synapse IDs which start with syn. All submissions have a `Submission` and `SubmissionStatus` object.

##### Web

Navigate to a file in Synapse and click on **Tools** in the upper right-hand corner. Select **Submit To Challenge** to pick the challenge for your submission. Follow the provided steps to complete your submission.

<img style="width: 30%;" id="toobig" src="/assets/images/submit_file_to_challenge.png">

## View Submissions of an Evaluation Queue

Submissions can be viewed through leaderboard widgets on Wiki pages.

### Adding Leaderboard Widget

<img style="width: 80%;" src="/assets/images/add_leaderboard_widget.png">

### Configuring Leaderboard Widget

Submission annotations can be added to a SubmissionStatus object to be displayed. Each of these annotations can be set to either public or private. Private annotations are not visible unless the team or Synapse user has **Can Score** or **Admin** permissions on the Evaluation queue. Public annotations can be viewed by any team or user that have **Can View** permissions.

Once you click on **Leaderboard**, you will have to input your own query statement such as `select * from evaluation_9610091`. Remember, 9610091 should be replaced with your own Evaluation queue ID. To view all the columns available, click **Refresh Columns**.

<img style="width: 80%;" src="/assets/images/configure_leaderboard_widget.png">

Clicking **Refresh Columns** will add these default columns.

<img style="width: 80%;" src="/assets/images/leaderboard_columns.png">

#### Leaderboard renderers
The appearance of columns in a leaderboard can be modified by changing the renderer used. You can change this by changing the value for the 'Renderer' attribute when configuring the leaderboard widget. These are the available renderers:

* userid: Renders a Synapse user ID to a Synapse user profile badge
* date: Renders epochtime in milliseconds to local time.  The user can also select to show dates in UTC (in user settings) rather than local time.
* epochdate: Deprecated
* markdown link: Renders text added as Synapse Wiki Markdown
* synapseid: Renders any Synapse Entity ID to a clickable Synapse entity badge
* cancelcontrol: Renders a button that allows for the cancellation of submissions


### Saving Leaderboard Widget

If you are happy with your leaderboard configurations, save both the configurations and the Wiki page to visualize these updates.

<img style="width: 80%;" src="/assets/images/leaderboard_on_wiki.png">


### Submit to an Evaluation Queue from a Wiki Page

<img style="width: 20%;" src="/assets/images/add_submission_widget.png">

You may embed a `Submit To Evaluation` widget on a Wiki page to improve visibility of your Evaluation queue. The widget allows participants to submit to multiple Evaluation queues within a Project or a single Evaluation queue. 

Currently, this Wiki widget is required to submit Synapse Projects to an Evaluation queue. Synapse Docker repositories can not be submitted through this widget.

<img style="width: 80%;" src="/assets/images/submit_to_evaluation_widget.png">

The "Evaluation Queue unavailable message" is customizable.  A queue may appear unavailable to a user if: 

* The Project doesn't have any Evaluation queues.
* The user does not have permission to view a Project's Evaluation queues. Learn more about [sharing settings]({{ site.baseurl }}{% link _articles/sharing_settings.md %}).
* The Evaluation queue quota is set such that a user can not submit to the queue.  Learn more about [quotas]({{ site.baseurl }}{% link _articles/evaluation_queues.md%}#create-an-evaluation-queue).

# See Also

To learn how to create a Wiki page, please visit [the Wikis article]({{ site.baseurl }}{% link _articles/wikis.md %}).
