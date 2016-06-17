---
title: "Provenance"
layout: article
---

## Provenance

Reproducible research is a fundamental responsibility of scientists, but the best practices for achieving it are not established in computational biology. The Synapse “Provenance” system is one of many solutions you can use to make your work reproducible by you and others.

Provenance is a concept describing the origin of something; in Synapse it is used to describe the connections between workflow steps that derive a particular file of results. Data analysis often involves multiple steps to go from a raw data file to a finished analysis.  Synapse’s Provenance Tools allow users to keep track of each step involved in an analysis, and share those steps with other users. Synapse provides capabilities for tracking the relationship between digital assets (e.g. data, code, analytical results), regardless of the computing location on which the steps are executed.

[Pic illustrating an analysis workflow]

### The basic elements of Synapse provenance

The model Synapse uses for provenance is based on the [W3C provenance spec](https://www.w3.org/standards/techs/provenance#w3c_all) where items are derived from an **activity** which has components that were **used**  and components that were **executed**.  Think of the used items as input files and executed items as software or code.  Both used and executed can either be items in Synapse or URLs such as a link to a github commit or a link to specific version of a software tool.  

[Screen shot of web provenance editing]

### Using R, python, or bash
The Synapse clients for R, python, and bash support creation and editing of provenance relationships.

For example, in R, create a file:

```{r}
file <- File(path="filteredPathwayResults.txt", parentId="syn2367745")
```

Store it, indicating that another entity was used to create it.

```{r}
file <- synStore(file, used=list("syn2824593"))
```
Now, show the provenance relationship you created in the previous step:
```{r}
provenance <- generatedBy(file)
provenance
```

Details on using provenance:
<table class="markdown-table border text-align-center">
<tr><th>  Introduction  </th><th> Full docs  </th></tr>
<tr><td>[python](https://www.synapse.org/#!Synapse:syn1768504/wiki/56099)  </td><td>  [python docs](http://python-docs.synapse.org/index.html#provenance) </td></tr>
<tr><td>[R](https://www.synapse.org/#!Synapse:syn1834618/wiki/55486) </td><td>[R docs](http://r-docs.synapse.org/) </td></tr>
<tr><td></td><td>[bash docs](http://python-docs.synapse.org/CommandLineClient.html)    </td></tr>





