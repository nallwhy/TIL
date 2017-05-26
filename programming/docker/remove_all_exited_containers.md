## Remove all Exited containers

`docker rm $(docker ps -q -f status=exited)`

Reference: https://coderwall.com/p/zguz_w/docker-remove-all-exited-containers
