---
title: "Getting Started with Synapse"
layout: article
excerpt: A getting started guide for new users who are interested in learning about Synapse.
category: intro
order: 1
---

<script src='/assets/javascripts/words.js'></script>

<style>
#webTab {
    width: 90%;
}
</style>

# Get Started with Synapse

This getting started guide is for new users who are interested in learning about Synapse. By following this guide, you will learn fundamental Synapse features by performing some simple tasks. You’ll learn how to:

* Create your own project and add content to Synapse
* Provide a project narrative which lives along side the scientific artifacts of your work, via the Synapse `Wiki` tools
* Share your work with other Synapse users, teams of users, or make your work public
* Install one of the Synapse clients (R, Python or command line)
* Incorporate Synapse in your workflows to read shared content and upload analysis results

## What is Synapse?
Synapse is an open source software platform that data scientists can use to carry out, track, and communicate their research in real time. Synapse enables co-location of scientific content (data, code, results) and narrative descriptions of that work. Synapse has seeded a growing number of living [research projects](https://www.synapse.org/#!StandaloneWiki:ResearchCommunities) and [resources](https://www.synapse.org/#!StandaloneWiki:OpenResearchProjects) including [Sage/DREAM Challenges](http://dreamchallenges.org/).

[Sage Bionetworks](http://www.sagebase.org){:target="_blank"} provides Synapse services free of charge to the scientific community through generous support from various [funding sources](/articles/faq.html#how-is-synapse-funded){:target='_blank'}. Synapse hosts many living [research projects](https://www.synapse.org/#!StandaloneWiki:ResearchCommunities) and [resources](https://www.synapse.org/#!StandaloneWiki:OpenResearchProjects) including [Sage/DREAM Challenges](http://dreamchallenges.org/).

<br/>
Synapse operates under a complete [governance process](/articles/governance.html) that includes well-documented [Terms and Conditions of Use](https://s3.amazonaws.com/static.synapse.org/governance/SageBionetworksSynapseTermsandConditionsofUse.pdf?v=4){:target="_blank"}, guidelines and operating procedures, privacy enhancing technologies, as well as the right of audit and external reviews.

# Register for a Synapse Account

Anyone can browse public content on the Synapse web site, but in order to download and create content you will need to register for an account using an email address. You will receive an email message for verification to complete the registration process.

<a href="https://www.synapse.org/register" class="btn btn-primary">Register</a>{:target="_blank"}

Since Synapse can store human subject data that has sharing and use restrictions, before you can upload files you will need to take a quiz about what kinds of items can be shared in Synapse. To start this process:

<a href="https://www.synapse.org/#!Quiz:Certification" class="btn btn-primary">Become a Certified User</a>{:target="_blank"}

Explore our [accounts, certification and profile validation](/articles/accounts_certified_users_and_profile_validation.html) page to find out more information on the different levels of users.  

# Project and Data Management on Synapse

<img style="float: right" src="/assets/images/project_1.png">

Once you have a Synapse account you can start adding content. All Synapse content is organized in `Projects` where you can collaboratively access and share `Wikis` (narratives) and `Files`. Each `Project` also contains a `Discussion Forum`.

As an exercise we are going to create an example `Project`. Decide on a unique name for your `Project`. Since `Project` names must be unique in Synapse, let me suggest a project name for you:

**<span id='random_proj_name'>Foo</span>**<br/>

Use this project name in the example scripts below.

<script type="text/javascript">
var chance = window.Chance.Chance();
var myadj = chance.capitalize(chance.pickone(adjectives));
var mynoun = chance.capitalize(chance.pickone(nouns));
var new_random_string = "Project ".concat(myadj, " ", mynoun);

var randomProjNameElement = document.getElementById("random_proj_name");
randomProjNameElement.innerHTML = new_random_string;
</script>

{% tabs %}
    {% tab Web %}
Go to your [profile Page](https://www.synapse.org/#!Profile:v) and click the **Create Project** button
    {% endtab %}
{% endtabs %}
<br>

By default, your newly created `Project` is private; you are the only person who can access it and any content you include in it.  Later on we will share your created `Project` with other users.

Objects like `Files`, `Folders`, `Projects` created in Synapse are assigned unique identifiers which are used for unique reference (a Synapse ID) with the format `syn12345678`. 

If you want to find your project at a later time you can see your projects on your [profile page](https://www.synapse.org/#!Profile:v/projects).

# Organizing Data: creating Files and Folders

You can use the `Files` tab to share your project's data, code, results, and any other information. Synapse `Files` and `Folders` are identified by a unique identifier. Synapse `Folders` are used to organize content and can contain other `Folders` and `Files`.

To add a `Folder`, click on the `Files` tab, then use the Tools menu and select **Add New Folder**.

Pick a file to upload in the `Folder` you just created. Use the Tools menu and select **Upload or Link to File**. Use the Browse button to select the file, or drag and drop it to upload, and click Save.

To explore other features available for `Files` and `Folders`, read about [annotating files](/articles/annotation_and_query.html), [assigning DOIs](/articles/doi.html), [versioning](/articles/files_and_versioning.html), [provenance](/articles/provenance.html),and [sharing settings](/articles/access_controls.html).

# Adding a Wiki to your Project

The `Wiki` tab in a `Project` provides a space for you to write narrative content to describe your project. This `Wiki` can be organized with subpages and a table of contents. 

`Folders` and `Files` in your `Project` can also have a `Wiki`. You can use this `Wiki` to document the contents of the `Folder` or `File`, similar to a README.

`Wiki` pages are written with [Markdown](https://www.markdownguide.org/), a lightweight syntax for styling text on the web. In addition to standard Markdown, `Wiki` pages can contain customized content, including images, tables, code blocks, LaTeX formatted equations, and scholarly references. Synapse-specific widgets also allow users to embed dynamic content based on other resources stored in Synapse.

See the [Wiki](/articles/wikis.html) user guide for more information and examples.

Here we will create a `Wiki` for our project. From the project page, click the **Tools button** and choose **Edit Project Wiki**. Add some text describing your `Project`, and then click Save.

## Local Folder and File Sharing Settings

Access to `Files`, `Tables`, and `Folders` is controlled by the **Sharing setting** that you select for your project. You may also set individual Sharing settings for specific `Files`, `Tables`, or `Folders` within a `Project`.

# Provenance and Tracking Content

<img style="float:right" src="/assets/images/example_provenance.png">

Synapse provides advanced capabilities for formally tracking the relationship between digital assets (e.g. data, code, analytical results) through the Synapse provenance system. This aides in disseminating data and results in ways that other users can reproduce and reuse. Using provenance allows you to track your analysis history and communicate and share a sequence of processing steps. Provenance relationships can, for example, be specified between raw data, analysis code and results that occur in a complex processing pipeline, regardless of where it is run. The Synapse web services for managing provenance expose a general data model based on the [W3C Prov spec](http://www.w3.org/2011/prov/wiki/Main_Page){:target="_blank"}. Central to the design, users are not required to use a particular execution environment or workflow tool. Instead, provenance can be specified by inserting calls to the Synapse web service layer into their normal workflows to record activity; pipelines may be created through simple scripting or by using workflow execution engines. The provenance system allows users to branch off workflows at any point in prior analyses, while maintaining detailed records of data, code, and environment versions needed to reproduce the work.

Provenance is most easily specified when you are uploading or editing a file in Synapse. To specify the provenance you specify the files used as input and any files that were executed to generate the `File`. Both used and executed can be either an arbitrary URL such as a reference to a code commit on Github, a file stored on an FTP site or references to items in Synapse. Here we demonstrate how to add a figure to Synapse and indicate that code from https://github.com/Sage-Bionetworks/synapseTutorials was used to generate the figure from the data in the file `data/cell_lines_raw_data.csv` that we uploaded previously:

{% tabs %}

{% tab Command %}
{% highlight bash %}
synapse add images/plot_2.png --parentId=syn123  \
--used raw_data_file  \
--executed https://github.com/Sage-Bionetworks/synapseTutorials
{% endhighlight %}
{% endtab %}

	 {% tab Java %}
	{% highlight java %}
import org.sagebionetworks.repo.model.provenance.*;

Activity newActivity = new Activity();
newActivity.setName("plot distributions");
newActivity.setDescription("Generate histograms for demo");
Set<Used> used = new HashSet<Used>();
UsedEntity usedEntity = new UsedEntity();
usedEntity.setWasExecuted(false);
Reference fileEntityReference = new Reference();
fileEntityReference.setTargetId(rawDataFileEntity.getId());
usedEntity.setReference(fileEntityReference);
UsedURL usedURL = new UsedURL();
usedURL.setWasExecuted(true);
usedURL.setUrl("https://github.com/Sage-Bionetworks/synapseTutorials");
used.add(usedEntity);
used.add(usedURL);
newActivity.setUsed(used);
newActivity = synapseClient.createActivity(newActivity);
    {%endhighlight %}
	{% endtab %}

    {% tab Python %}
	{% highlight python %}
plot2 = File("images/plot_2.png", parent=results_folder)
plot2 = syn.store(plot2, used=raw_data_file,
	executed='https://github.com/Sage-Bionetworks/synapseTutorials')

	{% endhighlight %}
	{% endtab %}

    {% tab R %}
	{% highlight r %}
plot2 <- File(path="/images/plot2.png", parentId=resultsFolder$properties$id)
plot2 <- synStore(plotFileEntity, used=rawDataFile,
    executed='https://github.com/Sage-Bionetworks/synapseTutorials',
    activityName="plot distributions",
    activityDescription="Generate histograms for demo")
    {%endhighlight %}
	{% endtab %}

    {% tab Web %}
click the **Upload or Link to File** button on the Files tab to upload image/plot_2.png.  After uploading click the **Tools** button and chose **Edit Provenance**.
    {% endtab %}
{% endtabs %}

## More Guides

Find additional information and tutorials through our <a href="/articles/">User Guide</a>.
