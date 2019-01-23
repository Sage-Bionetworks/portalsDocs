---
title: "Getting Started with Synapse Clients"
layout: article
excerpt: Use Synapse programmatically.
category: intro
order: 2
---

# Introduction

Clients provide a way to use Synapse programmatically. This page shows you how to install and login to get you started. Packages to interface and access data within Synapse are available for: 

* Command Line
* Python
* R


## Command Line

The Synapse command line client is implemented in Python and comes with the Synapse Python package. To install the Synapse command line client, please make sure that you have `Python` and `pip` installed. 
[Instruction on `Python` installation](https://www.python.org/downloads/)
[Instruction on `pip` installation](https://pip.pypa.io/en/stable/installing/)

After installing `pip` and `python`, in your terminal (Mac OS or GNU/Linux) or Command Prompt (Windows), run the following command:
```
pip install synapseclient
```
```
synapseclient login "username" "password"
synapseclient -h
```

For more documentation on the command line client see [here](https://python-docs.synapse.org/build/html/CommandLineClient.html).

## Python

The `synapseclient` package See the [Python client docs](https://python-docs.synapse.org/build/html/index.html#more-information) for supported versions of Python. 

```
pip install synapseclient
```
[Python client](https://python-docs.synapse.org/build/html/index.html)

## R

The `synapser` package is available for R version 3.4 and 3.5.  

```
install.packages("synapser", repos=c("https://sage-bionetworks.github.io/ran", "http://cran.fhcrc.org"))
install.packages("synapser")
```

```
library(synapser)
synLogin("username", "password")
```

To connect to Synapse with stored login credentials, visit the `synapser` [Overview page](https://r-docs.synapse.org/articles/synapser.html). Visit the [`synapser` R docs](https://r-docs.synapse.org) for complete documentation.


# To Report an Issue 

Report client-specific issues or bugs at the [R client](https://github.com/Sage-Bionetworks/synapsePythonClient/issues), [Python and command line client](https://github.com/Sage-Bionetworks/synapser) Github Issues pages. 
