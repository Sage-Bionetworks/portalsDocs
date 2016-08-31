---
title: "Provenance"
layout: article
excerpt: Learn about how Synapse visualizes and tracks the relationships of files and projects for reproducibility.  
---

<style>
#image {
 width: 55%;
 border: 1px solid #1e7098;
}
</style>

## Provenance

Reproducible research is a fundamental responsibility of scientists, but the best practices for achieving it are not established in computational biology. The Synapse “Provenance” system is one of many solutions you can use to make your work reproducible by you and others.

Provenance is a concept describing the origin of something; in Synapse it is used to describe the connections between workflow steps that derive a particular file of results. Data analysis often involves multiple steps to go from a raw data file to a finished analysis.  Synapse’s Provenance Tools allow users to keep track of each step involved in an analysis, and share those steps with other users. 

### The basic elements of Synapse provenance


The model Synapse uses for provenance is based on the [W3C provenance spec](https://www.w3.org/standards/techs/provenance#w3c_all){:target="_blank"} where items are derived from an **activity** which has components that were **used**  and components that were **executed**.  Think of the used items as input files and executed items as software or code.  Both used and executed can either be items in Synapse or URLs such as a link to a github commit or a link to specific version of a software tool.  

The Synapse clients for command line, Python, and R support creating and editing of provenance relationships. The Web client allows editing of provenance once the file has been uploaded.

Below is a Synapse visualization of provenance relationships that is demonstrated in the following section using our programmatic and web clients. in this example, we have two scripts, one that generates random numbers and another that takes a list of numbers and computes their squares. The project's workflow looks like this:

<img id="image" src="/assets/images/provenanceWorkflowDemo.png">

<br/>

### Setting Provenance When Uploading a File

Let's assume that you have a script that generates a list of normally distributed random numbers. This will mean that you have a script file that was used to create a data file and both will be uploaded into Synapse. 
For example, you have an R script file called generate_random_data.R:

```
# generate_random_data.R
rnorm(100)
```

And you've saved the output to a data file called random_numbers.txt


```
# Using command line to save R script output to file
Rscript generate_random_numbers.R > random_numbers.txt
```


#### Add the script file to Synapse

For this example, we'll assume that the `Project` already exists ([*Wondrous Research Example* : syn1901847](https://www.synapse.org/#!Synapse:syn1901847/files/)). We'll add our code file and data file to this project, or in Synapse terminology, the project will be the parent of the new entities. 

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Add the script to Synapse
synapse add generate_random_data.py -parentId syn1901847 
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
import synpaseclient
syn = synapseclient.login()

# Add the script to Synapse
script_file = File(path="generate_random_numbers.py", parent="syn1901847")
script_file = syn.store(script_file)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
require(synapseClient)
synapseLogin()

# Add the script to Synapse
script_file <- File(path="generate_random_numbers.R", parentId="syn1901847")
script_file <- synStore(script_file)
{% endhighlight %}
{% endtab %}

{% tab Web %}
Navigate to the **Files** tab on the project and click on **Upload or Link to File**. In the resulting pop-up, click the **Choose File** button and select the file(s) you would like to upload.
{% endtab %}

{% endtabs %}

<br/>
As you upload files onto Synapse, the new entity's synId will be provided. For this example, the new synId for the uploaded script file will be `syn7205215`. 

```
##################################################
 Uploading file to Synapse storage 
##################################################
Uploading [--------------------]0.00%   0.0bytes/29.0bytes  generate_random_dataUploading [####################]100.00%   29.0bytes/29.0bytes (14.0bytes/s) generate_random_data.R Done...
    Created/Updated entity: syn7205215	generate_random_data.R
```


#### Add Provenance
As the random_numbers.txt file was generated from the above script we are going to specify this using provenance. 

There are a couple ways to set provenance information for a Synapse entity. The `used` and `executed` arguments specify resources used and code executed in the process of creating the entity. Code can be stored in Synapse(as we did in the previous step) or, better yet, linked by URL to a source code versioning system like GitHub or SVN. As an example, we'll specify 2 somewhat contrived sources of provenance:

1. Synapse entity by synId: syn7205215 
2. URL to a page describing [normal distributions](http://mathworld.wolfram.com/NormalDistribution.html){:target="_blank"}

<br/>

{% include note.html content="Currently, the web client does not support setting provenance when uploading a file." %}

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Set provenance using synId of the uploaded script (syn7205215) and the website referenced
synapse add random_numbers.txt -parentId syn1901847 -executed syn7205215 -used http://mathworld.wolfram.com/NormalDistribution.html 

# Alternatively in the command line client, you can specify a local path to a file in provenance if it has already been uploaded 
synapse add random_numbers.txt -parentId syn1901847 -executed ./generate_random_data.py -used http://mathworld.wolfram.com/NormalDistribution.html 
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
# Set provenance for data file generated by the script file
data_file = File(path="random_numbers.txt", parent="syn1901847")
data_file = syn.store(data_file, executed="syn7205215", used="http://mathworld.wolfram.com/NormalDistribution.html")
{% endhighlight %}

{% endtab %}

{% tab R %}
{% highlight r %}
data_file <- File(path="random_numbers.txt", parent="syn1901847")
data_file <- synStore(data_file, executed="syn7205215", used="http://mathworld.wolfram.com/NormalDistribution.html")
{% endhighlight %}
{% endtab %}

{% tab Web %}
Currently, the web client does not support setting provenance when uploading a file.
{% endtab %}

{% endtabs %}

Once the data file is uploaded, it will provide the synId assigned to it. In this case, the data file's synId is `syn7208917`.

<br/>

### Editing Provenance

To continue our example above, we'll now add some new results from our initial data file. We're going to take the results in random_numbers.txt and square them. Here's our script to square the numbers:

```
# square.R

# Get the file with the random numbers
random_numbers <- synGet("syn7208917")
random_numbers <- read.table(file=random_numbers@filePath, header=F, stringsAsFactors = F, row.names = 1)

# Square the numbers
lapply(random_numbers, function(x) x^2)

```

And we'll save the output to a data file, squares.txt, using command line:

```
# Using command line to save R script output to file
Rscript square.R > squares.txt
```



#### Add the code entity 

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Add code entity to Synapse
synapse add square.R -parentId syn1901847
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
# Add code entity to Synapse 
code_file = File(path="square.R", parentId="syn1901847")
code_file = syn.store(code_file)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# Add code entity to Synapse 
code_file <- File(path="square.R", parentId="syn1901847")
code_file <- synStore(code_file)
{% endhighlight %}
{% endtab %}

{% tab Web %}
Navigate to the **Files** tab on the project and click on **Upload or Link to File**. In the resulting pop-up, click the **Choose File** button and select the file(s) you would like to upload.
{% endtab %}

{% endtabs %}


#### Add the data entity and set provenance

{% tabs %}

{% tab Command %}
{% highlight bash %}
# Add the data entity to Synapse
synapse add squares.txt -parentId syn1901847 
# Set the provenance for newly created entity syn7209166
synapse set-provenance -id syn7209166 -executed syn7209078 -used syn7208917
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
# Add the data file to Synapse
data_file = File(path="squares.txt", parentId="syn1901847")
data_file = syn.store(data_file)

# Set provenance for newly created entity syn7209166
data_file = syn.setProvenance(data_file, activity = Activity(used = "syn7208917", executed = "syn7209078"))
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# Add the data file to Synapse
data_file <- File(path="squares.txt", parentId="syn1901847")
data_file <- synStore(data_file)

# Set provenance for newly created entity syn7209166
act <- Activity(name = "Squared numbers", used = "syn7208917", executed = "syn7209078")
generatedBy(data_file) <- act
{% endhighlight %}
{% endtab %}

{% tab Web %}
To update the provenance on a file, navigate to the `File's` tab and click on the `File` that you would like to update. Click on the **Tools** dropdown in the upper right hand corner and select **Edit Provenance**. In the resulting pop-up, enter the relevant information. 

<img src="/assets/images/editProvenance.png">

{% endtab %}

{% endtabs %}


### Getting and Viewing Provenance

To view the provenance relationships you've created:

{% tabs %}

{% tab Command %}
{% highlight bash %}
synapse get-provenance -id syn7209166
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
syn.getProvenance("syn7209166")
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
provenance <- generatedBy("syn7209166")
provenance
{% endhighlight %}
{% endtab %}

{% tab Web %}
Navigate to the `File's` page to view its provenance. Clicking on the triple dots above entities will expand it to show the `File's` full provenance.

<img id="image" src="/assets/images/expandProvenance.png">
{% endtab %}

{% endtabs %}

### Reusing an Provenance for Multiple Files

An `Activity` is a Synapse object that helps keep track of what objects were 'used' in an analysis step ... as well as what objects were generated. Thus, all relationships between Synapse objects and an `Activity` are governed by dependencies. That is, an `Activity` needs to know what it 'used' -- and outputs need to know what `Activity` they were 'generatedBy'. A couple of points for clarity:

* An `Activity` can 'use' many things (i.e. many inputs to an analysis)
* Many outputs can be 'generatedBy' the same `Activity`

If an activity isn't assigned to an entity and then stored, a separate graph will be created for each file that the activity generated. 
The following example is used to assign the same activity to multiple files resulting in one provenance graph: 

{% tabs %}

{% tab Command %}
{% highlight bash %}
Unfortunately, command line currently does not support assigning the same activity to multiple files.
{% endhighlight %}
{% endtab %}


{% tab Python %}
{% highlight python %}
# Code used to generate the file
code_file = syn.get("syn123456")

# Files used to generate the information
expr_file = syn.get("syn246810")
filter_file = syn.get("syn135791")

# Activity to assign to multiple files
act = Activity(name="filtering",
                used=[expr_file, filter_file],
                executed=code_file)
syn.store(final_file, activity=act)

# Get the activity now associated with an entity
act = syn.getProvenance(final_file)

# Now you can set this activity to as many files as you want (file1, file2, etc are Synapse Files)
file_list = [file_1, file_2, file_3]
file_list = map(lambda x: syn.store(x, activity=act), file_list)

{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# Code used to generate the file
codeFile <- synGet("syn123456")

# Files used to generate the information
expr_file = synGet("syn246810")
filter_file = synGet("syn135791")

# Activity to assign to multiple files
act <- Activity(name="filtering",
                used=list(
                  list(entity=codeFile, wasExecuted=T),
                  list(entity=exprFile, wasExecuted=F),
                  list(entity=filterFile, wasExecuted=F)))
finalFile <- synStore(finalFile, activity=act)

# Get the activity now associated with an entity
act <- synGetActivity(finalFile)

# Now you can set this activity to as many files as you want (file1, file2, etc are Synapse Files)
finalList <- c(file1, file2, file3)
finalList <- lapply(finalList, function(x) synStore(x, activity=act))

{% endhighlight %}
{% endtab %}

{% tab Web %}
Unfortunately, the web interface currently does not support assigning the same activity to multiple files.
{% endtab %}

{% endtabs %}


### Details on using provenance

{:.markdown-table}
| Full Docs |
| -- |
| [python docs](http://docs.synapse.org/python/)
| -- |
| [R docs](http://docs.synapse.org/r)
| -- | -- |
| [command line docs](http://docs.synapse.org/python/CommandLineClient.html) |



