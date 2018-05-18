---
title: Managing Custom Metadata in Scale
layout: article
excerpt: A vignette of how to update metadata in bulk using file views and programmatic clients.
category: inpractice
---

# Managing Custom Metadata in Scale

This vignette will string together some of the concepts from [Annotations and Queries](/articles/annotation_and_query.md) and [Views](/articles/views.md) in order to bulk **upload**, **edit**, and **delete** annotations on files. 

## Annotation dictionaries
The Sage Bionetworks Systems Biology and Computational Oncology teams maintain [annotation dictionaries](https://github.com/sage-bionetworks/synapseAnnotations) in GitHub. You can use the terms found in the synapseAnnotations GitHub repo as a starting point for you own annotations.

 <a href="https://github.com/sage-bionetworks/synapseAnnotations" target="_blank" class="btn btn-info btn-lg active" role="button" aria-pressed="true">Annotation Dictionaries</a>

## Before we begin...
For this tutorial to be most effective, we'll be making a couple of assumptions. Please ensure that you have: (1) a Synapse Account, and (2) the Python Client installed. If not, head on over to the [Getting Started](/articles/getting_started.md) article to learn how to register for a Synapse account and install the Python Client. All good? Great, let's get annotating!

## Step 1: Create a Manifest
The easiest way to batch upload the files with annotations is by using a function called `syncToSynapse` in our Python client. This function requires the use of a tab-delimited manifest which contains, at minimum, the columns `path` and `parent`. But the real magic happens when you start to add additional columns which are annotations. So for example, your manifest might have the following headers: `path`, `parent`, `specimenID`, `assay`, `species`, `platform`, and `fileFormat`. Let's break that down a bit:

**path**: is the local path to your file <br>
**parent**: is the Synapse ID (in the format syn123456) that the files will be uploaded to <br>
**specimenID**: is the unique identifier for each of your specimens <br>
**assay**: is the technology used to generate the data in this file (e.g. rnaSeq, ChIPSeq, wholeGenomeSeq, etc) <br>
**species**: is the species of your sample (e.g. Mouse, Human, Triceratops etc) <br>
**platform**: is hardware used to generate the data (e.g. HiSeq2500, Affy6.0, HoodDNASequencer, etc) <br>
**sex**: e.g. male or female <br>
**fileFormat**: is the type of file (e.g. fastq, R script, etc) <br>

And here it is in a visual example: 

{:.markdown-table}
| path | parent | specimenID | assay | species | platform | sex | fileFormat |
| --- | --- | --- | --- | --- | --- | --- | --- |
| /local/path/to/velociraptor_b.fastq | syn123 | blue_1 | wholeGenomeSeq | Velociraptor mongoliensis | HoodDNASequencer | female | fastq |
| /local/path/to/velociraptor_d.fastq | syn123 | delta_1 | wholeGenomeSeq | Velociraptor mongoliensis | HoodDNASequencer | female | fastq |

We'll **save** this file in a tab-delimited format. And now onto the next step!

## Step 2: 