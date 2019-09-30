---
title: "Getting Started with Synapse"
layout: article
excerpt: A getting started guide for new users who are interested in learning about Synapse.
category: intro
order: 1
---

# Get Started with Synapse

This guide is for new users who are interested in learning about Synapse. You will learn fundamental Synapse features by performing some common tasks:

* Create your own project and add content to Synapse
* Provide a project description alongside your materials via the Synapse `Wiki` tools
* Share your work with other Synapse users, teams of users, or the public

## What is Synapse?

Synapse is a collaborative research platform that allows individuals and teams to share, track, and discuss their data and analysis in projects. Synapse is built to work on the web. We provide access to Synapse features and services for programmers through a REST API, [Python client](https://python-docs.synapse.org/build/html/index.html), [command line client](https://python-docs.synapse.org/build/html/CommandLineClient.html), and [R client](https://r-docs.synapse.org/). 


Synapse hosts many [research projects](https://www.synapse.org/#!StandaloneWiki:ResearchCommunities) and [resources](https://www.synapse.org/#!StandaloneWiki:OpenResearchProjects). It also hosts crowdsourced competitions, including [DREAM Challenges](http://dreamchallenges.org/). [Sage Bionetworks](http://www.sagebionetworks.org) provides Synapse services free of charge to the scientific community through generous support from various [funding sources](/articles/faq.html#how-is-synapse-funded).

Synapse operates under a thorough [governance process](/articles/governance.html). This includes [Terms and Conditions of Use](https://s3.amazonaws.com/static.synapse.org/governance/SageBionetworksSynapseTermsandConditionsofUse.pdf?v=4), guidelines, and operating procedures.

## Create Your Account
Anyone can browse public content on the Synapse web site. To download and create content, you will need to [register for an account](https://www.synapse.org/register) using an email address. You will receive an email message for verification to complete the registration process.

## Getting Certified

Synapse is a data sharing platform approved for storing data from human subjects research. This requires special care and thought. To upload files, Sage Bionetworks requires you demonstrate awareness of privacy and security issues. 

You can complete this by taking a [Certification Quiz](https://www.synapse.org/#!Quiz:Certification).

## Project and Data Management on Synapse

Synapse `Projects` are online workspaces where researchers can collaborate and organize their work. Synapse supports all kinda of working groups: individuals, small teams, and large consortia.

To create a new `Project`:

1. Navigate to the User Menu and click on [`Projects`](https://www.synapse.org/#!Profile:v/projects).
2. Click the **Create a New Project** button.
3. Decide on a unique name for your `Project` and click Save.

Your projects [dashboard](https://www.synapse.org/#!Profile:v/projects) stores your collection of projects.

Read about [`Projects`](making_a_project.md) in the user guide.

By default, your newly created `Project` is private. You are the only person who can access it, including any content in it. Read about [`Sharing Settings`](/sharing_settings.html) to distribute your data to a broader audience.

## Synapse IDs

Synapse projects are assigned a Synapse ID, a globally unique identifiers used for reference with the format `syn12345678`. Often abbreviated to "synID", the ID of an object never changes, even if the name does.



## Organizing Data: creating Files and Folders

You can use the `Files` tab to upload data, code, results, and other information to your project. Synapse Folders are used to organize content and can contain other Folders and Files. Synapse `Folders` and `Files` are also assigned a unique identifier (Synapse ID).

To add a `Folder`:

1. Click on the Files tab.
1. Use the Tools menu and select **Add New Folder**.
1. Decide on a Folder name and click 'Save'.

To upload a file into that folder:

1.  Use the Tools menu and select **Upload or Link to File**.
1. Use the Browse button to select the file, or drag and drop it to upload and click Save.

To explore other features available for files and folders, read about [annotating files](/articles/annotation_and_query.html), [assigning DOIs](/articles/doi.html), [versioning](/articles/files_and_versioning.html), [provenance](/articles/provenance.html),and [sharing settings](/articles/access_controls.html).

## Adding a Wiki to your Project

A Wiki is a document that can be edited by multiple people on the web. The Wiki tab in a project provides a space to write a description. This Wiki can be organized with subpages and a table of contents. Folders and files in your project can also have a wiki. You can use the wiki to document the contents of the folder or file, similar to a README.

Wiki pages are written with [Markdown](https://www.markdownguide.org/), a lightweight syntax for styling text on the web. In addition to standard Markdown, `Wiki` pages can contain customized content, including images, tables, code blocks, LaTeX formatted equations, and scholarly references. Synapse Wiki widgets also allow you to embed content based on other resources stored in Synapse.

See the [Wiki](/articles/wikis.html) user guide for more information and examples.

Create a Project wiki:

1. From the project page, click the **Tools button** and choose **Edit Project Wiki**.
1. Add some text describing your project, and then click Save.

To add a wiki to a folder or file:

1. Click on the Files tab and navigate to the Folder or File.
1. Use the Tools menu and select **Edit Folder Wiki** or **Edit File Wiki**.
1. Add some text describing the folder or file, and then click Save.

## Local Folder and File Sharing Settings

By default, access to folders and files is controlled by the same **sharing settings** as the project. You may set different sharing settings for specific folders and files in a project.

You may share a `Project` with specific people or make it public.

1. Click on the **Project Settings** menu and select **Project Sharing Settings**.
1. Add individuals or teams with different permissions.

For more details, read the [How to Share Projects](/articles/access_controls.html#how-to-share-projects) section of the Sharing Settings and Conditions for Use instructions.

For instructions on changing sharing settings for `Folders` and `Files`, read the [Sharing Other Content](/articles/access_controls.html#sharing-other-content) section of the Sharing Settings and Conditions for Use instructions.

## More Guides

Find additional information in our <a href="/articles/">User Guide</a>.

For information on using Synapse programmatically, see the documentation for the [Python client](https://python-docs.synapse.org/build/html/index.html), [command line client](https://python-docs.synapse.org/build/html/CommandLineClient.html), and [R client](https://r-docs.synapse.org/)
