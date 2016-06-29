---
title: Annotations and Queries
layout: article
excerpt: Learn about what annotations are, how to assign and modify them, and how to query them for analysis. 
---

## Annotations
Annotations in Synapse are semi-structured metadata that can be added to entities - Projects, Files, and Folders.
The metadata could come from an existing ontology (controlled vocabulary such as the Gene Onotology (GO)), an agreed upon set of terms (e.g., describing the results of a sequencing pipeline), or completely free form (like a tag system).
The annotations can be used to systematically describe groups of entities, which provides a way to search and discover entities in Synapse.
In Synapse, annotations are simple key-value pairs: the key is the name of the annotation (generally the same across groups of entities) and the values change for each entity.

As an example, let's say you have a collection of alignment files in the BAM file format from an RNASeq experiment, each representing a sample and replicate.
As is common, much of this information may be encoded in the file name (e.g., `Sample1_ConditionA.bam`).
However, this makes it difficult to find specific groups of files, such as all replicates of `Sample1`.
Adding this information as Synapse annotations enables a more complete description of the contents of the file and allows for discovery.

Continuing this example, the annotations you may want to add are:

* `fileType = bam`
* `dataType = mRNA`
* `sample = 1`
* `condition = A`

You may have dozens (or thousands) of these files, and each one should get a consistent set of annotations (they all have the same keys: `fileType`, `dataType`, `sample`, and `condition`.)

If these `bam` files were part of a larger sample processing pipeline, you might have many of the same key-value pairs on different entities.
For example, if the `bam` files were generated from `fastq` files, all annotations would be the same except for `fileType = fastq`.
Now, you will be able to find all the files for a specific sample.



<br/>

### Types of Annotations

Annotations can be one of four basic types 

* Text
* Integer
* Floating point
* Date



<br/>

### How to assign annotations

It's easiest to add annotations when initially uploading the file.
This can be done using the command line client, the Python client, the R client, or from the Web.

{% tabs %}
	{% tab Command %}
		{% highlight bash %}
synapse store Sample1_ConditionA.bam --parentId syn00123 --annotations '{"fileType":"bam", "dataType":"mRNA"}'
		{% endhighlight %}
	{% endtab %}

	{% tab Python %}
		{% highlight python %}
entity = File(path="Sample1_ConditionA.bam",parent="syn00123")
entity.annotations = {"fileType":"bam", "dataType":"mRNA"}
syn.store(entity)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
entity <- File("Sample1_ConditionA.bam",parent="syn00123")
synSetAnnotations(entity) <- list(fileType = "bam", dataType = "mRNA")
entity <- synStore(entity)
		{%endhighlight %}
	{% endtab %}

{% endtabs %}

<br/>
However, if you haven't decided on the annotations to add yet, you can add and modify the annotations at a later time as well.

Using the R or Python clients facilitates batch and automated population of annotations across many files.
The Web client is useful when uploading a single file, or if a minor change needs to be made to annotations on a few files.

For the command line, Python, and R clients, you can manipulate annotations

{% tabs %}
	{% tab Command %}
		{% highlight bash %}
synapse set-annotations --id syn123 --annotations '{"fileType":"bam", "dataType":"mRNA"}'
		{% endhighlight %}
	{% endtab %}

	{% tab Python %}
		{% highlight python %}
entity = syn.get("syn123")

# Assigning ONLY one annotation
entity.fileType = 'bam'
entity['fileType'] = 'bam'
# Assigning a set of annotations
entity.annotations = {"fileType":"bam", "dataType":"mRNA"}

syn.store(entity, forceVersion = F)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}

entity <- synGet("syn123")

# Assigning ONLY one annotation
synSetAnnotation(entity, "filType") <- "bam"
# Assigning a set of annotations
synSetAnnotations(entity) <- list(fileType = "bam", dataType = "mRNA")

entity <- synStore(entity, forceVersion = FALSE)
		{%endhighlight %}
	{% endtab %}

{% endtabs %}

<br/>
On the web, adding annotations is as easy as clicking the `Annotations` button in the upper right corner, which is available from any Project, Folder, or File entity page.

<img src="/assets/images/annotation-button.png">

This pops up a table of all existing annotations. Click the `Edit` button to add, delete, or modify the annotations.

<img src="/assets/images/annotation-box.png">

Now, you are able to enter a key (the name of the annotation), select the type, and enter a value.
Lastly, click `Save` to store the annotations for this entity.

<img src="/assets/images/annotation-edit-box.png">



<br/>

## Queries

Queries in Synapse look SQL-like:

```
SELECT * FROM <data type> WHERE <expression>
```

where currently supported `<data type>`:

{:.markdown-table}
| \<data type\> | 
| --------- | 
| project   | 
| folder    |
| file      |
| entity    |

If you know the entity type you are looking for, searching in `project`, `file`, or `folder` is what you want.
To search over annotations of all entity types, use `entity`.

The `<expression>` section are the conditions for limiting the search. Below demonstrates some examples of limiting searches.

For complete information on how to form queries and the types of limiting that can be performed, see the [Synapse Query API](https://sagebionetworks.jira.com/wiki/display/PLFM/Repository+Service+API#RepositoryServiceAPI-QueryAPI).

Along with annotations added by users, every entity has a number of fields useful for searching. For a complete list, see [here](http://hud.rel.rest.doc.sagebase.org.s3-website-us-east-1.amazonaws.com/org/sagebionetworks/repo/model/Entity.html), but here are some really useful ones.

* `projectId` which project the entity is associated with
* `parentId`: where the entity resides (inside a folder/sub-folder; may also be the project if in the root folder) - useful for finding all files if you know they are in a specific folder



<br/>

### Finding files in a specific project

To find all files in a specific project, you need to know the `projectId`, which is a Synapse identifier (looks like `syn12345`).
For example, the TCGA Pan-Cancer Project has a `projectId` of syn300013.
So, the query to find all files and all annotations associated with this project would be:

```
SELECT * FROM file WHERE projectId=="syn300013"
```


<br/>

### Listing files in a specific folder

To list the files and annotations in a specific folder, you need to know the Synapse ID of the folder (for example syn1524884, which has data from TCGA related to melanoma). All entities in this folder will have a `parentId` of syn1524884.

So, the query to find all files and all annotations in this folder would be:

```
SELECT * FROM file WHERE parentId=="syn1524884"
```

If you wanted to find all the sub-folders in this folder, you would do:

```
SELECT * FROM folder WHERE parentId=="syn1524884"
```

If you wanted both files and folders, this would work:

```
SELECT * FROM entity WHERE parentId=="syn1524884"
```


<br/>

## How to query on annotations

Annotations are most useful for discovery of similar types of entities.
Essentially, all annotations across Synapse are stored in a large table that can be queried to find entities with annotations matching your own criteria.
While it can be useful to search for files that exist within an known project or folder, this requires that you know ahead of time where the files are.

If annotations have been diligently added to folders, they can be used to discover files of interest.
For example, you can identify all files annotated as `bam` files (`fileType = bam`) uploaded to Synapse with the following query:

{% include note.html content="You will only be able to query the files you currently have permission to access." %}

```
SELECT * FROM file WHERE fileType=="bam"
```

<br/>
Likewise, if you had put the mRNA-Seq related files described in the section above into a project (for example syn12345) with the described annotations, then you could find all of the files for `Condition A` for `Sample 1`:

```
SELECT * FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"
```

<br/>
Lastly, you may not be interested in all of the possible annotations present on files. If you query and only a subset of entities has a specific annotation, all other entities will have a blank value for that annotation in the query results. You can limit the annotations you want displayed - generally, you want to know the Synapse ID of the entities, the file name, and the annotations you are interested in.

```
SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"
```

<br/>

You can query by using one of the analytical clients (command line, Python, and R). 

Using the example above, queries can be performed using these clients

{% tabs %}
	{% tab Command %}
		{% highlight bash %}
synapse query 'SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"'
		{% endhighlight %}
	{% endtab %}

	{% tab Python %}
		{% highlight python %}
# Option 1 
result = syn.query('SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"')

# Option 2 (More robust way)
result = syn.chunckedQuery('SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"')
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
result <- synQuery('SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"')
		{%endhighlight %}
	{% endtab %}

{% endtabs %}

<br/>

Also, you can view the query results in a table on the wiki page.

On the wiki page, click `Tools` button in the upper right corner to edit the wiki.

<img src="/assets/images/query-wiki-tool.png">

A window will pop up where you can edit the wiki content. Click `Insert` and Choose `Table: Query on Files/Folders`.

<img src="/assets/images/query-edit-wiki.png">

Then enter your query in the box and click `Insert` button. Once you `Save` the wiki page, the results will be displayed as a table.

<img src="/assets/images/query-file-wiki.png">



<br/>

## How to download based on queries

You can also download files in a folder using queries. Currently this feature is only available in the command line client. For example, if you want to download all the files in a folder that has a synapse id of `syn00123`, use

```
synapse get -q 'SELECT * FROM file WHERE parentId == "syn00123"'
````



<br/>
