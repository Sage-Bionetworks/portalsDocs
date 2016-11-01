---
title: "Downloading Data"
layout: article
excerpt: Learn the best practices of finding and downloading files.
---

# Overview

Data in Synapse can be downloaded using the programmatic clients (Python, R, and command line) as well as the web client. 

## Downloading a File

Every entity in Synapse has a unique synID associated with it.  It can be found on every entity page next to `Synapse ID:`, starting with `syn` ending with numbers (ie. `syn00123`).
`Files` can be downloaded by using the `get` command. By default, the `File` downloaded will always be the most recent version.

For example, to get the experimental protocol file on [Adult Mouse Cardiac Myocyte Isolation](https://www.synapse.org/#!Synapse:syn3158111){:target="_blank"} (syn3158111) from the [Progenitor Cell Biology Consortium (PCBC)](https://www.synapse.org/#!Synapse:syn177310){:target="_blank"} you would run the following:


{% tabs %}

{% tab Command %}
{% highlight bash %}
synapse get syn3158111
{% endhighlight %}
{% endtab %}

{% tab Python %}
{% highlight python %}
entity = syn.get("syn3158111")
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
entity <- synGet("syn3158111")
{%endhighlight %}
{% endtab %}

{% endtabs %}

<br/>

#### Versions

If there are multiple versions of a `File`, a specific version can be downloaded by passing the `version` parameter.

In this example, there are multiple versions of an [miRNA FASTQ file](https://www.synapse.org/#!Synapse:syn3260973){:target="_blank"} (syn3260973) from PCBC. To download the first version, you use the following:

{% tabs %}
{% tab Command %}
{% highlight bash %}
synapse get syn3260973 -v 1
{% endhighlight %}
{% endtab %}
{% tab Python %}
{% highlight python %}
entity = syn.get("syn3260973", version=1)
{% endhighlight %}
{% endtab %}
{% tab R %}
{% highlight r %}
entity <- synGet("syn3260973", version=1)
{%endhighlight %}
{% endtab %}

{% endtabs %}

<br/>

See [versioning](http://docs.synapse.org/articles/versioning.html) for more details.


#### Download Location

By default, for the Python and R clients, the download location will always be in the Synapse cache whereas the command line client downloads to your current working directory. In each case you can specify the `downloadLocation` parameter.

{% tabs %}
{% tab Command %}
{% highlight bash %}
synapse get syn00123 --downloadLocation /path/to/folder
{% endhighlight %}
{% endtab %}

{% tab Python %}
{% highlight python %}
entity = syn.get("syn00123", downloadLocation="/path/to/folder")
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
entity <- synGet("syn00123", downloadLocation="/path/to/folder")
{%endhighlight %}
{% endtab %}

{% endtabs %}

## Finding Files

Files in projects can be annotated to facilitate finding them with the information from the metadata tables. Most projects will have a page dedicated to the types of annotations available for query. 

For example, to find all files in a project with synID `syn00123` and fileType `bam`:

{% tabs %}

{% tab Command %}
{% highlight bash %}
synapse query "select * from file where projectId=='syn00123' AND fileType=='bam'"
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
import synapseclient
syn = synapseclient.Synapse()
syn.login()
results = syn.query("select * from file where projectId=='syn00123' AND fileType=='bam'")
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
library(synapseClient)
synapseLogin()
results <- synQuery("select * from file where projectId=='syn00123' AND fileType=='bam'")
{% endhighlight %}
{% endtab %}

{% endtabs %}


#### Download Tables

Please view [here](http://docs.synapse.org/articles/tables.html#making-changes-to-tables) to learn how to use `Tables`.


#### Download Wikis

The structure of a project's `Wiki` page can be extracted through the R and Python clients.  The id, title and parent `Wiki` page of each sub-`Wiki` page is also determined through the same method.


{% tabs %}

{% tab Python %}
{% highlight python %}
wiki = syn.getWikiHeaders("syn00123")
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
entity <- synGet("syn00123")
wiki <- synGetWikiHeaders(entity)
{%endhighlight %}
{% endtab %}

{% endtabs %}


The Markdown and other information of a `Project` sub-`Wiki` page can be obtained by knowing the id of the `Wiki`. The `Wiki` page id can either be obtained through the above method or can be found in the URL "www.synapse.org/#!Synapse:syn00123/wiki/**12345**" where 12345 is the `Wiki` page id. 


{% tabs %}

{% tab Python %}
{% highlight python %}
wiki = syn.getWiki("syn00123", 12345)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
entity <- synGet("syn00123")
wiki <- synGetWiki(entity, 12345)
{%endhighlight %}
{% endtab %}

{% endtabs %}



<!--#### Command Line Download-->

<!--The Synapse command line client offers two ways of downloading Synapse `Files` that the other clients do not.  First, it allows for recursive downloading of files, maintaining the folder structure that is present on Synapse.  -->

<!--```-->
<!--# syn00123 has to be a Folder or a Project-->
<!--synapse get --recursive syn00123-->
<!--```-->

<!--Second, users can pass in a [query statement](http://docs.synapse.org/articles/annotation_and_query.html#queries) to specify files to download.-->

<!--```-->
<!--# In the case below, syn00123 has to be a Project.  Any query statement would work. -->
<!--synapse get --query 'select id from entity where projectId == "syn00123"'-->
<!--```-->
