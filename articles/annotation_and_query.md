---
title: Annotations and Queries
layout: article
excerpt: Learn about using custom metadata, how to assign and modify annotations, and how to query them for analysis. 
category: howto
---

<style>
#image {
    width: 75%;
}
</style>

# Annotations

Annotations in Synapse are semi-structured custom metadata that can be added to `Projects`, `Files`, `Folders`, and `Tables` to further describe the object in question. Annotations can be based on an existing ontology or controlled vocabulary, or can be created in an <i>ad hoc</i> manner and modified later as the metadata evolves. Annotations can be a powerful tool used to systematically group and/or describe things (files or data, etc.) in Synapse, which then provides a way for those things to be searched for and discovered.

Annotations are structured as key-value pairs: the key is the name of the annotation while the value provides specifics. For example, if you have uploaded a collection of alignment files in the BAM file format from an RNA sequencing experiment, each representing a sample and experimental replicate, you can use annotations to add this information to each file in a structured way. Sometimes, users encode this information in file names, e.g., `Sample1_ConditionA.bam`, which makes it "human-readable" but makes it difficult to search for in a systematic way, such as finding all replicates of `Sample1`. Adding this information as Synapse annotations enables a more complete description of the contents of the `File`. 

In this case, the annotations you may want to add might look like this: 

* `assay = RNA-seq`
* `fileType = bam`
* `sample = 1`
* `condition = A`

For the second sample in the same experimental set with the same conditions, the annotations would have the same "keys" but slightly different "values", such as:

* `assay = RNA-seq`
* `fileType = bam`
* `sample = 2` (note that we've changed the value here but the rest are the same)
* `condition = A`

 If these samples were part of a dataset with multiple assays, such as RNA-seq and ATAC-seq, you would annotate the file entities with either `assay = RNA-seq` or `assay = ATAC-seq`. 

## Types of Annotations

Annotations can be one of four basic types 

* Text (Character Limit = 256)
* Integer
* Floating Point
* Date (Date and Time stored as a Timestamp)

You cannot have duplicate annotation keys on the same object in Synapse. 

### How to Assign Annotations

Annotations may be added when initially uploading a file, or at a later date. This can be done using the command line client, the Python client, the R client, or from the Web. Using the analytical clients facilitates batch and automated population of annotations across many files. The Web client is useful when uploading a single file, or if a minor change needs to be made to annotations on a few files.

#### Adding Annotations 

{% tabs %}
	{% tab Command %}
		{% highlight bash %}
synapse store Sample1_ConditionA.bam --parentId syn00123 --annotations '{"fileType":"bam", "assay":"RNA-seq"}'
		{% endhighlight %}
	{% endtab %}

	{% tab Python %}
		{% highlight python %}
entity = File(path="Sample1_ConditionA.bam",parent="syn00123")
entity.annotations = {"fileType":"bam", "assay":"RNA-seq"}
syn.store(entity)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
entity <- File("Sample1_ConditionA.bam", parent="syn00123")
entity <- synStore(entity)
synSetAnnotations(entity, annotations=list(fileType = "bam", assay = "RNA-seq"))
		{%endhighlight %}
	{% endtab %}
	
	{% tab Web %}
To add annotations through the web client, click the `Annotations` button in the upper right corner on a Project, Folder, or File page.

<img src="/assets/images/annotation-button.png">
	{% endtab %}
{% endtabs %}

<br/>

#### Modifying Annotations
If you have not decided on the annotations to add yet, you can add and modify the annotations at a later time as well, and you can manipulate annotations that have already been uploaded.


{% tabs %}
	{% tab Command %}
		{% highlight bash %}
synapse set-annotations --id syn123 --annotations '{"fileType":"bam", "assay":"RNA-seq"}'
		{% endhighlight %}
	{% endtab %}

	{% tab Python %}
		{% highlight python %}
entity = syn.get("syn123")

##### Modifying ONLY one annotation

entity.fileType = 'bam'
entity['fileType'] = 'bam'

##### Modifying a set of annotations

entity.annotations = {"fileType":"bam", "assay":"RNA-seq"}

syn.store(entity, forceVersion = F)
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}

entity <- synGet("syn123")

##### Modifying ONLY one annotation
synSetAnnotation(entity, annotations=list(filType = "bam"))

##### Modifying a set of annotations
synSetAnnotations(entity, annotations=list(fileType = "bam", assay = "RNA-seq")

		{%endhighlight %}
	{% endtab %}
	
	{% tab Web %}
Click the `Edit` button in the resulting table to add, delete, or modify annotations.
Start by entering a Key (the name of the annotation), select the type (text, integer etc.,), and enter the Value. For example Key=assay - Value=RNA-seq. Click `Save` to store the annotations for this entity.
To enter multiple Values for a single Key click `Enter` with the cursor in the Value field.
<img src="/assets/images/annotation-edit-box.png">

	{% endtab %}
{% endtabs %}

<br/>


# Queries

Queries in Synapse look SQL-like:

```
SELECT * FROM <data type> WHERE <expression>
```

where currently supported `<data type>` are:

{:.markdown-table}
| \<data type\> | 
| --------- | 
| project   | 
| folder    |
| file      |
| entity    |

If you know the entity type you are looking for, searching in `Project`, `File`, or `Folder` is what you want.
To search over annotations of all entity types, use `Entity`.

The `<expression>` section are the conditions for limiting the search. Below demonstrates some examples of limiting searches.

For complete information on how to form queries and the types of limiting that can be performed, see the [Synapse Query API](https://sagebionetworks.jira.com/wiki/display/PLFM/Repository+Service+API#RepositoryServiceAPI-QueryAPI).

Along with annotations added by users, every entity has a number of fields useful for searching. For a complete list, see [here](http://hud.rel.rest.doc.sagebase.org.s3-website-us-east-1.amazonaws.com/org/sagebionetworks/repo/model/Entity.html). 

Here are some really useful ones:

* `projectId` which project the entity is associated with
* `parentId`: where the entity resides (inside a folder/sub-folder; may also be the project if in the root folder) - useful for finding all files if you know they are in a specific folder



<br/>

### Finding files in a specific project

To find all files in a specific `Project`, you need to know the `projectId`, which is a Synapse identifier (looks like `syn12345`).
For example, the TCGA Pan-Cancer Project has a `projectId` of syn300013.
So, the query to find all files and all annotations associated with this `Project` would be:

```
SELECT * FROM file WHERE projectId=="syn300013"
```


<br/>

### Listing files in a specific folder

To list the `Files` and annotations in a specific `Folder`, you need to know the Synapse ID of the `Folder` (for example syn1524884, which has data from TCGA related to melanoma). All entities in this `Folder` will have a `parentId` of syn1524884.

So, the query to find all `Files` and all annotations in this `Folder` would be:

```
SELECT * FROM file WHERE parentId=="syn1524884"
```

If you wanted to find all the sub-folders in this `Folder`, you would do:

```
SELECT * FROM folder WHERE parentId=="syn1524884"
```

If you wanted both `Files` and `Folders`, this would work:

```
SELECT * FROM entity WHERE parentId=="syn1524884"
```


<br/>

### Queries on annotations

Annotations are most useful for discovery of similar types of entities. Essentially, all annotations across Synapse are stored in a large table that can be queried to find entities with annotations matching your own criteria. While it can be useful to search for files that exist within an known project or folder, this requires that you know ahead of time where the files are.

If annotations have been diligently added to `Files`, they can be used to discover files of interest.
For example, you can identify all `Files` annotated as `bam` files (`fileType = bam`) uploaded to Synapse with the following query:

{% include note.html content="You will only be able to query the files you currently have permission to access." %}

```
SELECT * FROM file WHERE fileType=="bam"
```

<br/>
Likewise, if you had put the RNA-seq related files described in the section above into a project (for example syn12345) with the described annotations, then you could find all of the files for `Condition A` for `Sample 1`:

```
SELECT * FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"
```

<br/>
Lastly, you can query on a subset of entities that have a specific annotation. You can limit the annotations you want displayed as following.

```
SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"
```

<br/>

Queries can be constructed using one of the analytical clients (command line, Python, and R) and on the web client, query results can be displayed in a table on a wiki page. Using the example above this can be done as following:

{% tabs %}
	{% tab Command %}
		{% highlight bash %}
synapse query 'SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"'
		{% endhighlight %}
	{% endtab %}

	{% tab Python %}
		{% highlight python %}


result = syn.chunkedQuery('SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"')
		{% endhighlight %}
	{% endtab %}

	{% tab R %}
		{% highlight r %}
result <- synQuery('SELECT id,name,dataType,fileType FROM file WHERE projectId=="syn12345" AND sample=="1" AND condition=="A"')
		{%endhighlight %}
	{% endtab %}
	
	{% tab Web %}	
On the wiki page, click `Tools` button in the upper right corner to `Edit Wiki`.
Click `Insert` and choose `Table: Query on Files/Folders`.
Enter your query in the box and click the **Insert** button. Once you save the wiki page, the results will be displayed as a table.

<img id="image" src="/assets/images/query-file-wiki.png">
    {% endtab %}
{% endtabs %}

<br/>

## How to download based on queries

You can download files in a folder using queries. Currently this feature is only available in the command line client. For example, if you want to download all files in a folder that has a synapse id of `syn00123`, use

```
synapse get -q 'SELECT * FROM file WHERE parentId == "syn00123"'
````

### See Also
[Downloading Data](/articles/downloading_data.html), [Tables](/articles/tables.html)
