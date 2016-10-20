---
layout: post
title: "Setting Up Local Docker Registry With UI"
markup: "rst"
---

Here is how to run a docker registry locally for a custom deployment, 
local management, or development. 

I found this useful when running Kubernetes and specifing a remote registry 
that i could develop and push images to quickly for testing. 

## Run docker regsitry

``` bash
docker run -d --restart always -e SEARCH_BACKEND=sqlalchemy -p 5000:5000 -v /home/cp16net/registry:/var/lib/registry --name docker-registry registry
```

## Run a docker registry ui

Find the docker ip of the registry.

``` bash
docker inspect -f '{{json .NetworkSettings.IPAddress}}' docker-registry
```

Use the ip to set the ENV for the UI to use.
Set the port you want to expose the UI on, here it will be [http://localhost:8500](http://localhost:8500)

``` bash
docker run -d -e ENV_DOCKER_REGISTRY_HOST=172.17.0.2 -e ENV_DOCKER_REGISTRY_PORT=5000 -p 8500:80 --name registry-frontend konradkleine/docker-registry-frontend:v2
```
