---
title: Links
layout: article
excerpt: The basics of creating, and modifying links on Synapse.
category: howto
---

<style>
#image {
    width: 50%;
}
</style>


# Links
Synapse `Links` provide users the ability to create a link to any file, table, folder, or project on Synapse. 



## Creating a Link


{% tabs %}

{% tab Python %}
{% highlight python %}
import synapseclient
syn = synapseclient.login()
linkEnt = synapseclient.Link(targetId="syn12345",targetVersion=1, parent="syn2345")
#targetId is the synapse id of the file, table, etc that you want to link
#targetVersion is optional, if no version is defined, the link will always point to the newest version
#parent is the folder or project where you want to link to exist
syn.store(linkEnt)

{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
library(synapser)
synLogin()

# Add a local file to an existing project (syn12345) on Synapse
linkEnt <- Link(targetId="syn12345",targetVersion=1, parent="syn2345")
linkEnt <- synStore(linkEnt)
#targetId is the synapse id of the file, table, etc that you want to link
#targetVersion is optional, if no version is defined, the link will always point to the newest version
#parent is the folder or project where you want to link to exist
{% endhighlight %}
{% endtab %}

{% tab Web %}
Navigate to the file, table, folder or project you want to save a link of. Click Tools and Save Link to...
<br>
<img id="image" src="/assets/images/save_link_to_file.png">
<br>

Select a folder or project that you want to save the link to (This feature is more like bookmarking the file to a specific location).
<br>
<img id="image" src="/assets/images/link_to_parent.png">
<br>

The final result looks like.
<br>
<img id="image" src="/assets/images/link_entity.png">
<br>

{% endtab %}
{% endtabs %}


### See Also
[Annotations and Queries](/articles/annotation_and_query.html), [Downloading Data](/articles/downloading_data.html), [Files and Versioning](/articles/versioning.html)
