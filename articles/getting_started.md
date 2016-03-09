---
title: "Getting Started with Synapse"
layout: article
---

## Getting started with Synapse using R

Import the synapse R client and log in to Synapse using locally stored credentials. New users have to supply username and password or their Synapse session API key

{% highlight r %}

library(synapseClient)
synapseLogin()
{% endhighlight %}



#### Create a Synapse Project to store your work:

{% highlight r %}
random_string <- paste(sample(LETTERS,4),collapse="")
proj_name <- paste('Demo Synapse Project',random_string,sep='-')
myProject <- Project(name=proj_name)
myProject <- synStore(myProject)
print(paste('Created a project with Synapse id', myProject$properties$id, sep = ' '))
{% endhighlight %}

#### Or, start with an existing project, such as the one created above:


{% highlight r %}
id = myProject$properties$id
myProject = synGet(id)
{% endhighlight %}

#### See your project online:


{% highlight r %}
onWeb(myProject)
{% endhighlight %}

#### Create a wiki for the project and put some text on it:

{% highlight r %}
placeholderText = "Place-holder text: Credibly innovate granular internal or organic sources whereas high standards in web-readiness. Energistically scale future-proof core competencies vis-a-vis impactful experiences. Dramatically synthesize integrated schemas with optimal networks."
wiki = WikiPage(owner=myProject, title="Analysis summary", markdown=placeholderText)
wiki = synStore(wiki)
{% endhighlight %}


#### Organize the project by creating folders within it:

{% highlight r %}
myFolderEntity = Folder(name = "plots", parentId = myProject$properties$id)
myFolderEntity = synStore(myFolderEntity)
{% endhighlight %}

#### See your project online:

{% highlight r %}
onWeb(myProject)
{% endhighlight %}

#### Create and upload a plot to the project:

{% highlight r %}
x = rnorm(500,mean=6,sd=4)
y = rnorm(500,mean=2,sd=3)
png(file="demo_plot.png")
par(mfrow = c(1,2))
hist(x, col = "red", xlim = range(-10,15))
hist(y, col = "blue", xlim = range(-10,15))
dev.off()

plotFileEntity = File(path="demo_plot.png", parentId=myFolderEntity$properties$id)
synSetAnnotations(plotFileEntity) = list(sampleType="iPSC", institution="FredHutch", protocol="A43.6")
plotFileEntity = synStore(plotFileEntity)
{% endhighlight %}



#### Add provenance describing how plot was created:
{% highlight r %}
plotFileEntity = synStore(plotFileEntity, 
                          executed='https://github.com/Sage-Bionetworks/synapseTutorials/blob/master/R/1.Synapse_R_API_demo.Rmd', 
                          activityName=" demo plot distributions", 
                          activityDescription="Generate histograms for demo",forceVersion=F)
{% endhighlight %}


#### View project on web:

{% highlight r %}
onWeb(plotFileEntity)
{% endhighlight %}


