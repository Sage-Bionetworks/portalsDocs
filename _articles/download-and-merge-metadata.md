---
title: Download Data Programmatically
layout: article
excerpt: Use R, Python or the command line to download data.
category: tutorials
---

All files in Synapse are automatically assigned a globally unique identifier used for reference with the format `syn12345678`. Often abbreviated to “synID”, the ID of an object never changes, even if the name does. In order to download data programatically, you need a list of synIDs that correspond to the files.

## Identify Files of Interest

Once you have identified the files you want to download from Explore Data, **Export Table** from Download Options.
<img style="width: 30%;" src="/assets/images/export-table-viz.png" alt="alt text">

You may chose to download the file as a *.csv* or *.tsv*. Files are named *Job-####.csv*, where # includes a long set of numbers. Move this file to your working directory to proceed with the following steps. Options to download data are available in the [R client]({{ site.baseurl }}{% link _articles/download-and-merge-metadata.md %}#r), [command line client]({{ site.baseurl }}{% link _articles/download-and-merge-metadata.md %}#command-line) and [Python client]({{ site.baseurl }}{% link _articles/download-and-merge-metadata.md %}#python).

## Download Files

### R

[Install the Synapse R client](https://r-docs.synapse.org/#installation) `synapser` to download data from Synapse and the R package `data.table` to perform fast data manipulations. [Login](https://r-docs.synapse.org/articles/manageSynapseCredentials.html#manage-synapse-credentials) to Synapse.

```
synapser::synLogin()
```
Read the exported table into R, create a directory to store files and download data using `synGet`. If `downloadLocation` is not specified, the files are downloaded to a hidden directory called `/.synapseCache`.

```
exported_table <- data.table::fread("Job-1342324092830598.csv")
dir.create("files")
lapply(exported_table$id, function(x) synapser::synGet(x,
                                                       downloadLocation = "./files"))
```




### Command Line

### Python
