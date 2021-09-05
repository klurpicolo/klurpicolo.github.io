---
layout: post
title:  "Dockerfile"
date:   2021-09-05 13:30:00 +0700
categories: devops
tags: [devops, docker]
---

# Dockerfile instruction
Instruction is information on how to build docker image.

### FROM
FROM image:tag AS alias
FROM node:14 AS build-image
- FROM initializes a new build stage and base image for subsequent instructions. Images can be pull from - public or private repository.
- FROM can appear mutiple times to used for make a build stage that can be copy and use on the final stage.

### WORKDIR
WORKDIR part
WORKDIR /path/to/workdir
- This set the working directory inside docker(also create directory). This will affect the rest instruction that refer to directory.

### COPY
COPY . /app
COPY source_dir destination_dir
- This copy file from outside of docker into inside

### ADD
APP . /app
APP source_dir destination_dir
- This is extended from COPY. There is 2 other ways to import to docker that copy way.

### ENV
ENV endpoint=http://loaclhost:8080
ENV key=value
- This set environment variable inside docker to be the given value.

### ARG
ARG key=default-value
ARG pet=cat
- This defind the variable that user can pass when exeucte "docker build" and we can also defind the default value to be used in case that user omitted the value.

### RUN
RUN apt-get update && apt-get install git
RUN command (shell form)
RUN ["executable", "param1", "param2"] (exec form)
- RUN usually used for install package required for application to run.

### CMD
CMD ["echo", "Hello World"]
CMD ["executable", "param1", "param2"] (exec form)
CMD echo "Hello World"
CMD command param1 param2 (shell form)
- CMD main purpose is to provides default for an executting container. CMD can be overriden by arguments when execute "docker run".

### ENTRYPOINT
ENTRYPOINT ["echo", "Hello World"]
ENTRYPOINT ["executable", "param1", "param2"] (exec form)
ENTRYPOINT echo "Hello World"
ENTRYPOINT command param1 param2 (shell form)
- This works similar to CMD but the difference is that command and params aren't ignored when run container with passing command and params. ENTRYPOINT and CMD can work together as ENTRYPOINT-> should execute anyway command and CMD -> command default args.

### EXPOSE
EXPOSE 8080
EXPOSE port
- This will expose the specified port on container with TCP as default protocal. User can use this port later when run container to forwards request into container.
