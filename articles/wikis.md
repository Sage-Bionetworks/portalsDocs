---
title: "Synapse Wikis"
layout: article
---

##Overview

Wikis are used in Synapse projects to provide a space to build narrative content to describe the research. Every project has a Wiki tab where you can build pages and a hierarchy of subpages as you would with any website. Wikis can also be added to folders and files allowing additional content documentation. Wikis, whether they are under the Wiki tab or on a folder, are built in the same way and enables incorporation of highly customized content including, but not limited to: images, tables, code blocks, LaTeX formatted equations, and scholarly references. In addition, Synapse-specific widgets lets you embed dynamic content based on other resources stored in Synapse. (needs highlight). Be aware that Access Controlls are not available for Wiki content. Wikis should therefore not 

##Starting, editing and deleting a Wiki
###Using the Synapse web portal
After creating a new project select the Wiki tab. Start a Wiki through the Tools menu by selecting the 'Edit Project Wiki'function. Content in this first Wiki becomes your projects home page. Go to the Tools menu to add subpages to your Wiki. These will appear as links on the left side of your home page (Image). Adding a wiki to a folder or file is done in a similar manner by selecting 'Edit Folder/File Wiki'. Content added to a Wiki can be Previewed before Saving. Each version of a saved Wiki is visible under Wiki History where older versions can be restored. To delete a Wiki select 'Delete Wiki Page' under Tools.  

###Using R/Pyton
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

##Wiki Features

###Markdown langauge
The layout and text of a Wiki can be customized using Wiki markdown language. A Formating Guide is available within the Wiki editing window. For additional markdown functions see (need link). Useful markdown shortcuts are available such as heading, bold, italic, strike-through, code block, sub and supescript. 

###Attachements
Files, images and videos can be attached to a Wiki. This may be content on from the web, your desktop, or files already uploaded to Synapse. Be aware that Controlled Access (link) can not be applied to 


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

