---
title: "File Views"
layout: article
excerpt: Use file views to see files across multiple projects and folders.
category: howto
---

<style>
#image {
    width: 90%;
}
</style>


# Overview 
A file view is a view of all `Files` within one or more `Projects` or `Folders`. File views can:

 * Provide a way of isolating or linking data based on similarities
 * Provide the ability to link `Files` together by their annotations
 * Allow view/editing `File` attributes in bulk
 * Allow `Files` to be easily searched and queried
 
 <br/>


## Create a File View

To create a file view, navigate to your `Project` in the web client. Here, we'll use [*The Wondrous Research Example*](https://www.synapse.org/#!Synapse:syn1901847/). Navigate to the **Table** tab and click on the **Add File View** button. 
 
<img id="image" src="/assets/images/addFileView.png">

In the resulting pop-up, give your view a name and then select **Add container** under **Scope** to select the `Projects` and `Folders` you'd like to use. 

<img id="image" src="/assets/images/fileViewPopup.png">

You can search for `Projects`/`Folders` of interest by browsing by your favorite and current projects, by searching for a project by name, or by entering in a Synapse Id. Click on the Project name to add it to your scope. You can select specific folders in a project by clicking on the caret.

<img id="image" src="/assets/images/expandProject.png">

Clicking on a `Project` or `Folder` will select it for the view. 

<img id="image" src="/assets/images/selectProject.png">

The **Scope** section will now show each `Project` or `Folder` that you've selected. You can continue to add as many more containers as you'd like by using the **Add container button**. In this example, we've selected a total of 3 containers: 2 `Projects` (One Project to Rule Them All and the Wondrous Research Example), and a `Folder` (BAM) within the PCBC C4 Raw Data mRNA folder. Click **Next** to continue on and define the schema you'd like to use for your file view. 

<img id="image" src="/assets/images/seeAllSelectedContainers.png">

By default, all the file metadata will be populated. At the bottom, you can click the **Add All Annotations** button to populate every annotation across the scope as columns. If you'd like to enable faceted search on these columns, select **Values** or **Range** from the dropdowns under the **Facet** option. You can remove and reorder the columns as you'd like. If you remove any default columns that you'd like to restore, you can click the **Add Default View Columns**. 
Click **Next** to create the file view.

<img id="image" src="/assets/images/setFacetSearch.png">

## Query a File View
A file view can be queried exactly the same as any other `Table` in Synapse. Please see [Tables](/articles/tables.html) for more examples.

### Using Simple Search
The file views are in Simple Search mode by default. You can filter out `Files` of interest by selecting what characteristics you like using the facet menu on the left. You can toggle between simple and advanced search using the `Show advanced search/Show simple search` link.

<img id="image" src="/assets/images/fileViewFacetedSearch.png">


### Using Advanced Search
In advanced search, you can use a SQL-like query to search for files in that view. In the example below, we're selecting for all files that have a `Cell Type` of `PSC`. 

<img id="image" src="/assets/images/fileViewAdvancedSearch.png">

## Insert a View into a Wiki
File views can also be placed inside a `Wiki` once they have been created. You can embed the entire file view or a subset of a query on it. 

To insert a file view with a synId of `syn8146547`:

In the **Edit Project Wiki** window, select **Table: Query on a Synapse Table/View** under the **Insert** dropdown. To embed the entire file view into the wiki enter `SELECT * FROM syn8146547` in the resulting pop-up.


To embed a subset of the file view, like the advanced search query in the previous example, enter `SELECT * FROM syn8146547 WHERE Cell_Type = 'PSC'`. 

<img id="image" src="/assets/images/subsetFileVIewWiki.png">


**Save** the query and the edits to the `Wiki` to embed the file view.


## See Also
[Annotations and Queries](/articles/annotation_and_query.html), [Tables](/articles/tables.html)
