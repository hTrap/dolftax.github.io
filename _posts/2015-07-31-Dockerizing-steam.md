---
layout: post
category : General
title : "Dockerizing sTeam"
tagline: ""
tags : [Docker, GSoC, sTeam]
---

I am currently working with [sTeam collaboration platform](http://societyserver.org/Topics/sTeam/Interface-elements-for-Document-Management) as a GSoC dev under FOSSASIA umbrella.

sTeam has a lot of depencencies. A lot! One major issue faced by developers was version conflict between dependencies. Docker seemed to solve this issue. Docker is a great image distribution model for server templates. It uses `btrfs` (a copy-on-write filesystem) to keep track of filesystem diff's which can be committed and collaborated on with other users (like git). It also has a central repository of disk images that allow you to easily run different operating systems and shares the host kernel.

In this post, I will explain the workflow of containerizing sTeam with Docker.

> Prepend  `sudo`

- Install docker on host system, start & enable the docker.service

```
dnf install docker
systemctl start docker
systemctl enable docker
```

- Pull a base image from docker hub

> Note: It is upto you which image to use. I am using Ubuntu as base image.

```
docker pull ubuntu:latest
```

- List the images to verify the pull

```
docker images
```

.. should display `ubuntu  latest  xxxxxxxxxxxx  x months ago  x MB`

- Build your own image

```
docker build -t="dolftax/steam"
```

- Lets run bash to install sTeam itself and its dependencies

```
docker run -t -i dolftax/steam /bin/bash
```

- Install the packages and its dependencies.

In my case, sTeam server. Installation steps - [https://github.com/societyserver/sTeam/wiki/Installation-steps#manual](https://github.com/societyserver/sTeam/wiki/Installation-steps#manual)

- Grab latest container ID. The first one would be the recently closed container.

```
docker ps -a
```

- Commit the changes so that [you don't lose the data when container exits](https://stackoverflow.com/questions/19585028/i-lose-my-data-when-the-container-exits)

```
docker commit [container-id] dolftax/steam:v1
```

You should get a long hash as the success message

> Note: v1 is a [tag](https://docs.docker.com/reference/commandline/tag/) | Don't use `latest` tag. [Don’t be tempted by it](https://medium.com/@mccode/the-misunderstood-docker-tag-latest-af3babfd6375).

- Create a docker hub account and login

```
docker login
```
.. which is self explanatory.

- Push the image to docker hub (Before that, create a [docker hub](https://hub.docker.com/account/signup/) account and `docker login`)

```
docker push dolftax/steam
```

Done!

.. after containerizing with docker, sTeam installation is as easy as

```
docker pull dolftax/steam:v1
```

Try containerizing your project and you would love it.
