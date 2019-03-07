---
title: "Getting Started with Synapse"
layout: article
excerpt: A getting started guide for new users who are interested in learning about Synapse.
category: intro
order: 1
---

# Get Started with Synapse

This guide is for new users who are interested in learning about Synapse. Here you will learn fundamental Synapse features by performing some common tasks. You’ll learn how to:

* Create your own project and add content to Synapse
* Provide a project description which lives alongside your materials, via the Synapse `Wiki` tools
* Share your work with other Synapse users, teams of users, or make your work public

## What is Synapse?

Synapse is an open source platform that can be used to carry out, track, and communicate research. Synapse allows scientific content (data, code, results) and descriptions of that work to be stored in the same location. Synapse hosts a growing number of [research projects](https://www.synapse.org/#!StandaloneWiki:ResearchCommunities) and [resources](https://www.synapse.org/#!StandaloneWiki:OpenResearchProjects) including [Sage/DREAM Challenges](http://dreamchallenges.org/).

[Sage Bionetworks](http://www.sagebionetworks.org) provides Synapse services free of charge to the scientific community through generous support from various [funding sources](/articles/faq.html#how-is-synapse-funded){:target='_blank'}.

Synapse operates under a complete [governance process](/articles/governance.html) that includes [Terms and Conditions of Use](https://s3.amazonaws.com/static.synapse.org/governance/SageBionetworksSynapseTermsandConditionsofUse.pdf?v=4){:target="_blank"}, guidelines and operating procedures, privacy enhancing technologies, as well as the right of audit and external reviews.

## Register for a Synapse Account

Anyone can browse public content on the Synapse web site, but to download and create content you will need to register for an account using an email address. You will receive an email message for verification to complete the registration process.

<a href="https://www.synapse.org/register" class="btn btn-primary">Register</a>{:target="_blank"}

Synapse can store human subject data that has sharing and use restrictions. Before you can upload files you will need to take a quiz about what kinds of items can be shared in Synapse. To start this process:

<a href="https://www.synapse.org/#!Quiz:Certification" class="btn btn-primary">Become a Certified User</a>{:target="_blank"}

Explore our [accounts, certification and profile validation](/articles/accounts_certified_users_and_profile_validation.html) page for more information on the different levels of users.

## Project and Data Management on Synapse

Once you have a Synapse account you can start adding content. All Synapse content is organized in `Projects` where you can collaboratively access and share `Wikis` (descriptions of your Project) and `Files`. Each `Project` also contains a `Discussion Forum`.

As an exercise we are going to create an example `Project`. Go to your [projects list](https://www.synapse.org/#!Profile:v/projects) on your dashboard. Click the **Create Project** button. Decide on a unique name for your `Project` and click Save.

By default, your newly created `Project` is private; you are the only person who can access it and any content you include in it.  In another tutorial you will learn how to share your created `Project` with other users.

Objects created in Synapse, like `Files`, `Folders`, `Projects`,  are assigned a Synapse ID, unique identifiers used for reference with the format `syn12345678`.

To find your project at any time, you can see your projects on your [dashboard](https://www.synapse.org/#!Profile:v/projects).

## Organizing Data: creating Files and Folders

You can use the `Files` tab to share your project's data, code, results, and any other information. Synapse `Files` and `Folders` are identified by a unique identifier (Synapse ID). Synapse `Folders` are used to organize content and can contain other `Folders` and `Files`.

To add a `Folder`:

1. Click on the Files tab.
1. Use the Tools menu and select **Add New Folder**.
1. Decide on a Folder name and click 'Save'.

To upload a file into that folder:

1.  Use the Tools menu and select **Upload or Link to File**.
1. Use the Browse button to select the file, or drag and drop it to upload and click Save.

To explore other features available for `Files` and `Folders`, read about [annotating files](/articles/annotation_and_query.html), [assigning DOIs](/articles/doi.html), [versioning](/articles/files_and_versioning.html), [provenance](/articles/provenance.html),and [sharing settings](/articles/access_controls.html).

## Adding a Wiki to your Project

A Wiki is a document that can be edited by multiple people on the web. The `Wiki` tab in a `Project` provides a space for a description of your project. This `Wiki` can be organized with subpages and a table of contents.

`Folders` and `Files` in your `Project` can also have a `Wiki`. You can use the `Wiki` to document the contents of the `Folder` or `File`, similar to a README.

`Wiki` pages are written with [Markdown](https://www.markdownguide.org/), a lightweight syntax for styling text on the web. In addition to standard Markdown, `Wiki` pages can contain customized content, including images, tables, code blocks, LaTeX formatted equations, and scholarly references. Synapse Wiki widgets also allow you to embed content based on other resources stored in Synapse.

See the [Wiki](/articles/wikis.html) user guide for more information and examples.

Create a Project `Wiki`:

1. From the project page, click the **Tools button** and choose **Edit Project Wiki**.
1. Add some text describing your project, and then click Save.

To add a `Wiki` to a `Folder` or `File`:

1. Click on the Files tab and navigate to the Folder or File.
1. Use the Tools menu and select **Edit Folder Wiki** or **Edit File Wiki**.
1. Add some text describing the folder or file, and then click Save.

## Local Folder and File Sharing Settings

By default, access to `Folders` and `Files` is controlled by the **sharing settings** that the project has. You may also set individual sharing settings for specific `Folders` and `Files` within a `Project`.

You may share a `Project` with specific people or make it public. To do this click on the **Project Settings** menu and select **Project Sharing Settings**. For more details, read the [How to Share Projects](/articles/access_controls.html#how-to-share-projects) section of the Sharing Settings and Conditions for Use instructions.

For instructions on changing sharing settings for `Folders` and `Files`, read the [Sharing Other Content](/articles/access_controls.html#sharing-other-content) section of the Sharing Settings and Conditions for Use instructions.

## More Guides

Find additional information in our <a href="/articles/">User Guide</a>.

For information on using Synapse programmatically, see the documentation for the [Python client](https://python-docs.synapse.org/build/html/index.html), [command line client](https://python-docs.synapse.org/build/html/CommandLineClient.html), and [R client](https://r-docs.synapse.org/)
