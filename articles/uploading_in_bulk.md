---
title: Uploading Data in Bulk
layout: article
excerpt: Learn about uploading files and their metadata in bulk.
category: howto
---

# Overview

When uploading many files to Synapse, it can be helpful to do that all in one operation while setting all the metadata. By using the `sync` function in the `synapseutils` helper package, files can be uploaded in bulk with annotations and provenance set all at once. 
The files will be uploaded using a tab separated manifest file. In this article we will cover how to: 
	
* create a manifest 
* upload the files in bulk
* modify files in bulk using the manifest

<br/>

Read more about the helper functions on the **[synapseutils](http://docs.synapse.org/python/synapseutils.html#module-synapseutils)** page.

## Uploading Data in Bulk

#### Create a Manifest

Files can be uploaded in bulk by using a tab separated (.tsv) manifest file. The manifest file has multiple columns: a set of required columns, columns for provenance, and columns for annotations. See below for an example manifest template:

{:.markdown-table}
| path | parent | name | used | executed | annotation1 | annotation2 |
| --- | --- | --- | --- | --- | --- | --- |
| /path/to/file.csv | syn123 | Tardar Sauce | syn654 | https://github.com/your/code/repo | grumpy | cat |

<br/>

The above manifest describes a "file.csv" to upload to a folder/project `syn123` and name it "Tardar Sauce". It would have [provenance](/articles/provenance.html) indicating that the code (https://github.com/your/code/repo) was executed using entity `syn654` to generate your file. Additional [annotations](/articles/annotation_and_query.html), called `annotation1:grumpy` and `annotation2:cat` in this example, can be added to the file to make it easier to query and understand at a glance. Examples of annotations that could be placed on the file are fileFormat, cellType, study, etc. 

To review:
* the **path** and **parent** columns are required
* **used** and **executed** are for provenance and optional (but helpful!),
* **annotation1** and **annotation2** are for annotations and also optional (but also helpful!)

<br/>

Download the [template](/assets/downloads/example_manifest_template.tsv).

#### Validate the Manifest

The format of the manifest file (called 'manifest.tsv' in this example) can be validated prior to uploading by using the parameter `dry_run = True` in `syncToSynapse`:

{% highlight python %}
# Load required libraries
import synapseclient
import synapseutils

# login to Synapse
syn = synapseclient.login(email='me@example.com', password='secret', rememberMe=True) 

# validate the manifest
foo = synapseutils.syncToSynapse(syn, manifest_file='manifest.tsv', dry_run=True)
{% endhighlight %}

<br/>

#### Upload the Files

Using the validated manifest above, we can now upload the files to Synapse. Once the files have all uploaded, you will receive an email notification of the completed upload. It will also notify you if there were any errors that were encountered during upload. 

{% highlight python %}
# upload files using manifest
bar = synapseutils.syncToSynapse(syn, manifest_file='manifest.tsv')
{% endhighlight %}

<br/>



## Downloading Data in Bulk

Files can be downloaded in bulk using the `syncFromSynapse` function found in `synapseutils`. This function allows you to download all the files in a folder or project along with all the annotations and provenance on those files. If the files are being downloaded to a specific location outside of the Synapse Cache, it will create a manifest that can be used to upload those files back up to Synapse.

For example, to download all the files in `syn123` to a folder called "myFolder" on your local computer:

{% highlight python %}
# Load required libraries
import synapseclient
import synapseutils

# login to Synapse
syn = synapseclient.login(email='me@example.com', password='secret', rememberMe=True) 

# download all the files in folder syn123
all_files = synapseutils.syncFromSynapse(syn, entity='syn123', path='/path/to/myFolder')
{% endhighlight %}


## Editing in Bulk

You can edit files in bulk by changing the values in the manifest and pushing it up to Synapse using the `syncToSynapse` function. The manifest allows you to modify everything: file path, provenance, annotations, and versions. However, if only annotations are being updated, we recommend using our [File Views](/articles/fileviews.html) feature. 


Please note that you cannot move things with a manifest. If the parentId is changed, it will create a copy and the file will exist in two different locations. 


{% include note.html content="Changing the parent synId in a manifest creates a copy of the file. It does not move it." %}


### See Also
[Downloading Data](/articles/downloading_data.html), [Provenance](/articles/provenance.html), [Annotations and Queries](/articles/annotation_and_query.html), [File Views](/articles/fileviews.html), [Files and Versioning](/articles/files_and_versioning.html)
