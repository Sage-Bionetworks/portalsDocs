---
title: "Synapse Wikis"
layout: article
---

##Synapse Wiki pages

Wiki pages contain highly customized content including, but not limited to images, tables, code blocks, LaTeX formatted equations, and scholarly references. Synapse-specific widgets also allow users to embed dynamic content based on other resources stored in Synapse 

###Creating Wiki Content
It is possible to have a Wiki page for every project, folder and file. For folders and files, the Wiki pages are not visible until there is content. 

{% tabs %} {% tab Command %}

{% highlight bash %} 
The command line client does not support the creation of Wiki content. We suggest using (to get to the webpage of the project) synapse onweb syn### where syn### is the Synapse Id of your created project. Then editing the Wiki using the web client. {% endhighlight %} {% endtab %}

{% tab Python %} {% highlight python %}
projWiki = Wiki(title='Data Summary', owner = myProj ) markdown = '''* Cell growth look normally distributed
There is evidence of inverse growth between these two cell lines ''' projWiki['markdown'] = markdown projWiki = syn.store(projWiki) 
{% endhighlight %} {% endtab %}

{% tab R %} {% highlight r %} library(synapseClient); 
placeholderText <- "* Cell growth look normally distributed\n* There is evidence of inverse growth between these two cell lines." wiki <- WikiPage(owner=myProject, title="Analysis summary", markdown=placeholderText) wiki <- synStore(wiki) 
{%endhighlight %} {% endtab %}

{% tab Web %} Select **Tools** then select **Edit Project/Folder/File wiki** {% endtab %}

{% endtabs %}

###Available Wiki Features
Synapse Wikis provide the ability to richly describe project, files and folders within synapse.  

####Markdown langauge
Wiki markdown language has many capabilities to customize the layout and text of the Wiki. For full capabilities of the markdown language see the [help document](https://www.synapse.org/#!Wiki:syn2467792/ENTITY).

####Synapse Widgets
In addition to textual descriptions of a project Synapse also provides the ability to customize a wiki with specific widgets.  

 * Table of contents
To summarize the contents of a Wiki. This will, by default, include the primary wiki page and any subpages added to the primary Wiki page. The Table of Contents will be displayed on the left and can be re-ordered by clicking 'Edit Order' under the table of contents. 

 * Table Widgets
 There are many ways to add tabular data to the Wiki page.
  * Paste tabular data
  
  The easiest way [add how to, I have never figured it out]
  
  * Query on Synapse table
  
If you have an existing Synapse table related to this project you can query selected columns using this Synapse table widget.  To do so select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'Query on Synapse Table'. Once the widget opens you can type the query according the the [Synapse table query language](ISTHEREALINKFORTHIS?). 

  * Query on files/folders

You can also query specific files and folders.  To do so select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'Query on Files/Folders'. Once the widget opens you can type the query according the the [Synapse query language](). 

 * Genome Browser 
To add a genome browser region to the Wiki page, select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'Genome Browser'. 
 
 * File Preview

To preview a file on the Wiki page, select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'File Preview'. 

 * User

To link to a specific user profile on a Wiki page select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'User'. 

* Provenance graph

To show file provenance on a Wiki, select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'Provenance Graph'. 

 * Button Link

To use a button link on the Wiki page, select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'Button Link'. 

 * Entity List
 
To list a number of entities in a Wiki page select 'Edit Project Wiki' from the 'Tools' directory and from the 'Insert' directory select 'Entity List'. 

####Challenge-specific widgets
Sage is involved in many DREAM challenges that require specific functionality built into the Synapse Wiki. 
  * Join Team
  * Submit for Evaluation
  * Team Badge

###Wiki Versioning
We should describe how to revert back to older versions of the Wiki, if possible.  [I do not know enough about this!]

###Deleting a wiki
It is possible to remove a wiki from a File or Folder. Note: this is unrecoverable and all versions are deleted.  There are two ways to do this:
1. Select *Tools* and select *Delete Wiki Page*
2. Select *Tools* and select *Edit wiki* and then click the red 'Delete page' button.

