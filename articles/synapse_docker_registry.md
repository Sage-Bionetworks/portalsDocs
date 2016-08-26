---
title: Synapse Docker Registry
layout: article
excerpt: The Synapse Docker registry provides a space for synapse users to store and distribute their Docker images per Synapse project.  The Docker images will inherit the some access control settings as the project, so users can choose to develop the tool in private then share it after it is complete.
---

##Synapse Docker Registry
Docker containers wrap a piece of software in a complete filesystem that contains everything needed to run.  This can be extremely helpful as software can have many dependencies, so by installing all of them in a container, users can avoid going through the trouble of installing the software on their own computer.  These Docker images can then be stored and distributed on a Docker registry.  The Synapse Docker registry will allow users to create software on a per project basis which can be easily shared across synapse. To learn more about [Docker](https://www.docker.com/products/overview) and [Docker registry](https://www.docker.com/products/docker-registry)


### Creating a new Docker image
Lets begin by creating a custom docker image.  Users can choose to either modify an existing docker image or build a docker image from a Dockerfile.  Docker images must be tagged with 'docker.synapse.org/synapseProjectId/myreponame' to allow images to be saved. 

**Tagging an existing docker image to save onto the synapse registry**

```
docker pull ubuntu
```
To tag an existing docker image, users must know the IMAGE ID.  The IMAGE ID can be found by doing:
```
docker images
#REPOSITORY	TAG	IMAGE ID	CREATED	SIZE
#ubuntu	latest	f8d79ba03c00	6 days ago	126.4 MB
```
Tag the docker image:
```
docker tag f8d79ba03c00 docker.synapse.org/syn12345/mytestrepo:version1 
#syntax: docker.synapse.org/<projectId>/<repoName>:<tag>
```
You can also choose to not tag your image with anything, which will by default tag it with `latest`.
```
docker tag f8d79ba03c00 docker.synapse.org/syn12345/mytestrepo
```

**Build your own image from a Dockerfile**
When building a Docker image from a Dockerfile simply add a `-t` to the docker build command with the correct Synapse Docker registry tag.
```
docker build -t  docker.synapse.org/syn12345/my-repo path/to/dockerfile
```
To learn more about building [docker images](https://docs.docker.com/engine/getstarted/step_four/).  

### Storing Docker images in Synapse
To store Docker images, use the `docker push` command.  To push to the Synapse Docker Registry, users must be logged into the registry:

```
docker login docker.synapse.org
#Username: (Input Synapse username)
#Password: 
#Login Succeeded 
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
```
docker pull docker.synapse.org/syn12345/my-repo
#By default, if you do not specify a tag, it will attach "latest" as the tag.  If you specified a tag on your repository, be sure to pull the repository with the tag.
docker pull docker.synapse.org/syn12345/mytestrepo:version1
```



