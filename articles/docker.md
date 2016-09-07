---
title: Synapse Docker Registry
layout: article
excerpt: The Synapse Docker registry provides a space for synapse users to store and distribute their Docker images per Synapse project.  The Docker images will inherit the some access control settings as the project, so users can choose to develop the tool in private then share it after it is complete.
---

## Synapse Docker Registry

Docker is a tool for creating, running and managing lightweight virtual machines, represented as versioned 'repositories.'  These virtual machines make it possible to distribute executable environments with all of the dependencies that can easily be run by others.  A Docker 'registry' is a collection of these repositories and there are a number of open registries on the web. Synapse hosts a private registry, freely available to our users. Synapse users interact with the Synapse Docker registry using the standard Docker client. As with Files and Table, Repositories are organized by project and inherit the access controls from the project.


### Creating a new Docker image
Users can choose to either modify an existing docker image or build a docker image from a Dockerfile.  Docker images must be tagged with 'docker.synapse.org/synapseProjectId/myreponame' to allow images to be saved.  In this example we will pull down an existing Docker image and add it to the Synapse project, 'syn12345'. 

**Tagging an existing docker image to save onto the synapse registry**

```
docker pull ubuntu
```

To tag an existing docker image, users can use the IMAGE ID or the repo name.  The IMAGE ID can be found by doing:

```
docker images
#REPOSITORY	TAG	IMAGE ID	CREATED	SIZE
#ubuntu	latest	f8d79ba03c00	6 days ago	126.4 MB
```

Tag the docker image:

```
docker tag f8d79ba03c00 docker.synapse.org/syn12345/mytestrepo:version1 
#or
docker tag ubuntu:latest docker.synapse.org/syn12345/mytestrepo:version1 
#syntax: docker.synapse.org/<projectId>/<repoName>:<tag>
```

You can also choose to not tag your image with an explicit tag, which will by default tag it with `latest`.

```
docker tag f8d79ba03c00 docker.synapse.org/syn12345/mytestrepo
```

**Build your own image from a Dockerfile**
When building a Docker image from a Dockerfile simply add a `-t` to the docker build command with the correct Synapse Docker registry tag.

```
docker build -t  docker.synapse.org/syn12345/my-repo path/to/dockerfile
```

Learn more about building [docker images](https://docs.docker.com/engine/getstarted/step_four/).  

### Storing Docker images in Synapse
To store Docker images, use the `docker push` command.  To push to the Synapse Docker Registry, users must be logged into the registry:

```
docker login -u <synapse username> -p <synapse password> docker.synapse.org
```

After logging in, view your images and decide which ones to push into the registry.

```
docker images
#REPOSITORY                                 TAG                 IMAGE ID            CREATED             SIZE
#docker.synapse.org/syn12345/mytestrepo   version1            f8d79ba03c00        6 days ago          126.4 MB
#ubuntu                                     latest              f8d79ba03c00        6 days ago          126.4 MB
#docker.synapse.org/syn12345/my-repo	latest	df323sdf123d	2 days ago	200.3 MB
docker push docker.synapse.org/syn12345/mytestrepo:version1
docker push docker.synapse.org/syn12345/my-repo
```

### Using Docker images stored in Synapse
To access the Docker images stored in Synapse, simply use the `docker pull` command.

{% include tip.html content="By default, if you do not specify a tag, it will attach latest as the tag.  If you specified a tag on your repository, be sure to pull the repository with the tag." %}
```
docker pull docker.synapse.org/syn12345/my-repo
```

Docker tags can be assigned to later commits. If you want to be explicit about the version of an image then instead of referencing a tag you can reference a digest:

```
docker pull docker.synapse.org/syn12345/mytestrepo@sha256:2e36829f986351042e28242ae386913645a7b41b25844fb39b29af0bdf8dcb63
```

where the digest for a commit is printed to the command line after a successful Docker push. The Synapse web portal displays current digests for a repository's tags on the repository's Synapse page.

{% include note.html content="You can add external repositories, i.e. repositories that live in other registries like DockerHub and quay.io. For these repositories there is no tight integration (Synapse doesn't contact these external registries) but it allows you to list Docker repositories that are relevant to the project but are not within Synapse.
" %}


