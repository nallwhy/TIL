## Docker Basics

https://docs.docker.com/engine/getstarted/

### Find and run the whalesay image

[docker/whalesay image](https://hub.docker.com/r/docker/whalesay/) on Docker Hub.

Run `docker run docker/whalesay cowsay boo` command.

The first time you run a software image, the docker command looks for it on your `local system`. If the image isn’t there, then docker gets it from the `hub`.

### Build your own image

#### Step 1: Write Dockerfile

A Dockerfile is a recipe which describes the *files*, *environment*, and *commands* that make up an image.

```
# The FROM instruction sets the Base Image for subsequent instructions.
FROM docker/whalesay:latest

# The RUN instructions will execute any commands in a new layer on top of the current image and commit the results.
RUN apt-get -y update && apt-get install -y fortunes

# The final command to run after its environment is set up.
CMD /usr/games/fortune -a | cowsay
```

#### Step 2: Build an image from your Dockerfile

```
docker build -t docker-whale .
```
The `-t` parameter gives your image a tag, so you can run it more easily later.
`.` tells the `docker build` command to look in the current directory for a file called `Dockerfile.

### Tag, push, and pull your image

#### Tag

```
docker tag <image ID> <account_name>/<image_name>:<version_or_tag>

# example
docker tag 7d94 nallwhy/docker-whale:latest
```

#### Login to Docker hub

```
docker login
```

#### Push

```
docker push nallwhy/docker-whale
```

#### Remove Image

```
docker rmi <image ID>
```

#### Pull

```
docker run nallwhy/docker-whale
```

#### Remove Container

```
docker rm <container ID>
```
