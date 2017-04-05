## Run docker in docker

http://stackoverflow.com/questions/43085429/run-docker-build-in-ubuntu16-04-docker/43088716#43088716

```
docker run --privileged -it dind /bin/bash
/usr/bin/dockerd -H unix:///var/run/docker.sock > dockerd.log 2>&1 &
```

So you may need to add `entrypoint` to start docker daemon in your `Dockerfile`.