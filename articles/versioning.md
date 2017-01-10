---
title: Files and Versioning
layout: article
excerpt: Uploading files and file versioning in Synapse.
category: howto
---

<style>
#image {
    width: 40%;
}
#largeImage { 
    width: 100%;
}
</style>

# Files

Synapse `Files` are like files on a local file system, except they are accessible to anyone who has access, can be annotated and queried on, can be embedded into Synapse `Wiki` pages, and can be associated with a [DOI](https://en.wikipedia.org/wiki/Digital_object_identifier){:target="_blank"}. `Files` carry the Conditions for Use of the Synapse `Folder` they are placed in, plus any additional specific Conditions for Use they have on their own.

By default, `Files` uploaded to Synapse are stored in 'Synapse Storage', which is freely available to you. `Files` can also be stored on your own Amazon S3 bucket (see [Custom Storage Locations](/articles/custom_storage_location.html)) as well as your own SFTP server. Furthermore, if you don't want to upload a file (it has external restrictions on sharing, is really large, for example) you can also link to the file. In this way, the file will be accessible through the Synapse clients when you are on the computer that the file is stored, but can be annotated, queried, and documented with a Wiki through Synapse. Lastly, you can provide web-accessible links (http or ftp) as Synapse files, which will redirect to that location. All of the same Synapse `File` features are available (e.g., annotations and Wikis) are available on external links as well.

Synapse `Files` (as well as `Folders` and `Projects`) are identified by a unique identifier called a Synapse ID. It takes the form `syn12345678`. This identifier can be used to refer to a specific file on the web and through the clients.

# Versioning

Versioning is an important component to reusable, reproducible research. There are a number of ways that versioning can be accomplished, including the commonly used filename modification scheme (e.g., 'file.txt', 'file-1.txt', 'file-1a.txt', 'file-final.txt', and then 'file-reallyfinal.txt'). However, this is less than satisfactory for a number of reasons. First, the rules for naming are arbitrary, and may change over time. Second, it is not possible to easily determine (without external documentation) that this set of file changes are related to the same file. Third, it becomes difficult to manage future use of specific versions of the file. Using `File` versioning provided by Synapse solves these issues.

### Details

After uploading a file to Synapse, you may find the need to change it. For example, you modified the code that creates the file, changing its contents. Or, you found an error and needed to make a manual change. Uploading new versions of a file to replace an existing one in Synapse is the answer.

It is important to note that, by default, any previous versions of the file should still be available - it may be used in provenance relationships or as part of a data release. To handle these types of situations, files re-uploaded to Synapse create a new version.


When a Synapse `File` is initially stored, it automatically gets a version of `1`. It can be referred to explicitly by its Synapse ID: `syn12345678.1`. If the contents of a file are changed and you indicate that you want to replace an existing Synapse `File` with a new one (through the web interface from the Tools menu by selecting 'Upload a New Version of the File', or through the programmatic clients), the Synapse ID will remain but the version will increase, e.g., `syn12345678.2`. Hence, this is a standard, transparent way to determine how a file has changed and the relationship over time between the versions. It also provides a single entry point (the Synapse ID, `syn12345678`) to find the file and determine if there are multiple versions. Further, it allows for downstream use of specific versions of the `File`, and other users can always come back to see if new versions exist and have been subsequently processed as well.

Providing the Synapse ID without any versioning information to any of the clients (e.g., `syn12345678`) will always point to the most recent version of the file. In this way, updates to files can be automatically fetched by users by simply omitting the version.

If a DOI has been created for a Synapse file, it is automatically versioned as well, so specific versions can be cited in other places.

The easiest way to create a new version of an existing Synapse `File` is to use the same file name and store it in the same location (e.g., the same `parentId`). Synapse will automatically determine that a new version of a file is being stored, only if the contents of the file have changed. If the contents have not changed (e.g., the `md5sum` of the file is identical to the most recent version), a new file will not be uploaded and the version will not increase.

Only the file and annotations information are included in the version. Other metadata about a Synapse `File` (such as the description, name, parent, ACL, *and its associated Wiki*) are not part of the version, and will not change between versions.

### Uploading a File
When you first upload a `File` to Synapse, it has a version of `1`. 

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Add a local file to an existing project (syn12345) on Synapse
synapse store raw_data.txt --parentId syn123456
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
import synapseclient
syn = synapseclient.login()

# Add a local file to an existing project (syn12345) on Synapse
file = File(path='/path/to/raw_data.txt', parent='syn12345')
file = syn.store(file)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
library(synapseClient)
synapseLogin()

# Add a local file to an existing project (syn12345) on Synapse
file <- File(path='/path/to/raw_data.txt', parentId='syn12345')
file <- synStore(file)
{% endhighlight %}
{% endtab %}

{% tab Web %}
Navigate to the **Files** tab of the project you would like to add the file to. Click on **Upload or Link to File** to upload a local file from your computer or to link to a URL (such as http or ftp).

<img id="image" src="/assets/images/upload_file_button.png">
{% endtab %}

{% endtabs %}


#### Uploading a New Version of a File
To upload a new version of a `File`, the easiest way to do this is to use the same file name and store it in the same location (e.g., the same `parentId`), therefore uploading a new version follows the same steps as uploading a file for the first time. **The only major difference is the practice of adding a comment to the new version in order to easily track differences at a glance**. The example file `raw_data.txt` will now have a version of `2` and a comment describing the change. 

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Upload a new version of raw_data.txt 
synapse store raw_data.txt --parentId syn123456 
#Currently there is no option to add a version comment when uploading via command line. We recommend adding the comment via the web client.
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
# Upload a new version of raw_data.txt 
from synapseclient import File

file = File(path='/path/to/raw_data.txt', parent='syn12345')
file.versionComment = "Added 5 random normally distributed numbers."
file = syn.store(file)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# Upload a new version of raw_data.txt
file <- File(path='/path/to/raw_data.txt', parentId='syn12345')
file@properties$versionComment <- "Added 5 random normally distributed numbers."
file <- synStore(file)
{% endhighlight %}
{% endtab %}

{% tab Web %}
Navigate to the file on Synapse and click the **Tools** button. Select **Upload A New Version Of The File** from the dropdown menu and upload or link to your file in the resulting pop-up. 

<img id="image" src="/assets/images/upload_new_version_file.png">

Once the new version has been uploaded, select the **File History** button and then **Edit Version Info** to add the version comment.

<img id="image" src="/assets/images/add_version_comment.png">

{% endtab %}

{% endtabs %}


#### Updating Annotations/Provenance Without Changing Versions
Any change to a `File` will automatically update its version. If this isn't the desired behavior, such as minor cahnges to the metadata, you can set `forceVersion=False` with the Python or R clients. For command line, the commands `set-annotations` and `set-provenance` will update the metadata without creating a new version. Adding/updating annotations and provenance in the web client will also not cause a version change.

{% include important.html content="Because Provenance is tracked by version, set forceVersion=False for minor changes to avoid breaking Provenance." %}

**Setting annotations without changing version**

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Set annotation on file (syn56789)
synapse set-annotations --id syn56789 --annotations '{"fileType":"bam", "assay":"RNA-seq"}'
{% endhighlight %}
{% endtab %}

{% tab Python %}
{% highlight python %}
# Get file from Synapse, set download=False since we are only updating annotations
file = syn.get('syn56789', download=False)
# Add annotations 
file.annotations = {"fileType":"bam", "assay":"RNA-seq"}
# Store the file without creating a new version
file = syn.store(file, forceVersion=False)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# Get file from Synapse, set download=False since we are only updating annotations
file <- synGet('syn56789', downloadFile=F)
# Add annotations 
synSetAnnotations(file) <- list(fileType = "bam", assay = "RNA-seq")
# Store the file without creating a new version
file = synStore(file, forceVersion=F)
{% endhighlight %}
{% endtab %}

{% tab Web %}
Please refer to the [Annotations and Queries](/articles/annotation_and_query.html) article for instructions on adding/editing annotations via the web client.
{% endtab %}

{% endtabs %}

<br/>

**Setting provenance without changing version**

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Setting provenance (syn56789)
synapse set-provenance -id syn56789 -executed ./path/to/example_code
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
# Get file from Synapse, set download=False since we are only updating provenance
file = syn.get('syn56789', download=False)
# Add provenance 
file = syn.setProvenance(file, activity = Activity(used = '/path/to/example_code'))
# Store the file without creating a new version
file = syn.store(file, forceVersion=False)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# Get file from Synapse, set download=False since we are only updating annotations
file <- synGet('syn56789', downloadFile=F)
# Add provenance 
act <- Activity(name = 'Example Code', used = '/path/to/example_code')
generatedBy(file) <- act
# Store the file without creating a new version
file = synStore(file, forceVersion=F)
{% endhighlight %}
{% endtab %}

{% tab Web %}
Please refer to the [Provenance](/articles/provenance.html) article for instructions on adding/editing annotations via the web client.
{% endtab %}

{% endtabs %}

### Downloading a Specific Version of a File
By default, the `File` downloaded will always be the most recent version. However, a specific version can be downloaded by passing the `version` parameter.

{% tabs %}
{% tab Command %}
{% highlight bash %}
# Retrieve the first version of a file from Synapse
synapse get syn56789 -v 1
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

{% tab Web %}
Navigate to where the file is stored in Synapse and click the **File History** button to show a list of all versions. Select the version you could like to download and once the page has refreshed, click the blue **Download** button next to the name of the file.

<img id='largeImage' src='/assets/images/download_specific_version.png'>
{% endtab %}

{% endtabs %}

<br/>

### See Also
[Provenance](/articles/provenance.html), [Annotations and Queries](/articles/annotation_and_query.html), [Downloading Data](/articles/downloading_data.html)