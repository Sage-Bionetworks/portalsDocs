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

To create a file view, select the `Project` that you would like to create the view in. The `Project` you choose does not have to contain the files you are creating the view of.

{% tabs %}

{% tab Python %}
{% highlight python %}
# load library
import synapseclient
from synapseclient import EntityViewSchema

# login to Synapse
syn = synapseclient.login()

# define your scope, you can do this by getting the entity with "syn.get" or by using just the synId
# two folders will be defined in this scope using both methods
folder1 = syn.get('syn111')
folder2 = 'syn222'

# create a view named "My Fileview" to upload to project syn333
entity_view = EntityViewSchema(name='My Fileview', parent='syn333', scopes=[folder1, folder2], view_type='file')

# store the view in Synapse
entity_view = syn.store(entity_view)

{% endhighlight %}
{% endtab %}

{% tab Web %}
<iframe width="560" height="315" src="" frameborder="0" allowfullscreen></iframe>
{% endtab %}

{% endtabs %}
 

## Query a File View
A file view can be queried exactly the same as any other `Table` in Synapse. Please see [Tables](/articles/tables.html) for more examples.

{% tabs %}

{% tab Command %}
{% highlight bash %}
# query for everything in syn123
synapse query 'SELECT * FROM syn123'
{% endhighlight %}
{% endtab %}

{% tab Python %}
{% highlight python %}
# query for everything in syn123
import synapseclient
syn = synapseclient.login()
query = syn.tableQuery('SELECT * FROM syn123')
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# query for everything in syn123
library(synapseClient)
synpaseLogin()
query <- synTableQuery('SELECT * FROM syn123')
{% endhighlight %}
{% endtab %}

{% tab Web %}

See the [Using Simple Search](/articles/fileviews.html#using-simple-search) and [Using Advanced Search](/articles/fileviews.html#using-advanced-search) sections below.
{% endtab %}

{% endtabs %}

<br/>

## Update Annotations in Bulk

File views can be used to update annotations in bulk. To update other metadata in bulk, such as provenance, please see the [Uploading Data in Bulk](/articles/uploading_in_bulk.html) article.

For example, if you would like to add the annotation `dogSays`:`woof` to every file in a fileview with the synId syn456, you can do:

{% tabs %}

{% tab Python %}
{% highlight python %}
# load libraries
import pandas as pd
import synapseclient
from synapseclient import table

# login
syn = synapseclient.login()

# query from everything in syn456
foo = syn.tableQuery('select * from syn456')

# convert to dataframe for easier handling
bar = foo.asDataFrame()

# add in annotation as a column with key: dogSays, value: woof
bar['dogSays'] = 'woof'

# store the fileview with the new annotation in Synapse
fv = syn.store(synapseclient.Table(foo.tableId, bar))

{% endhighlight %}
{% endtab %}

{% tab Web %}

<iframe width="560" height="315" src="" frameborder="0" allowfullscreen></iframe>

{% endtab %}

{% endtabs %}



### Using Simple Search
The file views are in Simple Search mode by default. You can filter out `Files` of interest by selecting what characteristics you like using the facet menu on the left. You can toggle between simple and advanced search using the `Show advanced search/Show simple search` link.

<img id="image" src="/assets/images/fileViewFacetedSearch.png">


### Using Advanced Search
In advanced search, you can use a SQL-like query to search for files in that view. In the example below, we're selecting for all files that have a `Cell Type` of `PSC`. 

<img id="image" src="/assets/images/fileViewAdvancedSearch.png">

## Insert a View into a Wiki
File views can also be placed inside a [`Wiki`](/articles/wikis.html) once they have been created. You can embed the entire file view or a subset of a query on it. 

To insert a file view with a synId of `syn8146547`:

In the **Edit Project Wiki** window, select **Table: Query on a Synapse Table/View** under the **Insert** dropdown. To embed the entire file view into the wiki enter `SELECT * FROM syn8146547` in the resulting pop-up.


To embed a subset of the file view, like the advanced search query in the previous example, enter `SELECT * FROM syn8146547 WHERE Cell_Type = 'PSC'`. 

<img id="image" src="/assets/images/subsetFileViewWiki.png">


**Save** the query and the edits to the `Wiki` to embed the file view.


## See Also
[Annotations and Queries](/articles/annotation_and_query.html), [Tables](/articles/tables.html), [Wikis](/articles/wikis.html)
