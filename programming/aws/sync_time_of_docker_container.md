## Sync time of docker container

This issue will be fixed in Docker for mac **17.06**. 🎉

https://github.com/docker/for-mac/issues/17#issuecomment-300734810

---

One day, I tried to let my docker container download a file from AWS S3 via AWS CLI, but it failed!

```bash
$ aws s3 cp <s3-path> <file-path>
fatal error: An error occurred (403) when calling the HeadObject operation: Forbidden
```

I found [an issue about this situation](https://forums.docker.com/t/time-in-container-is-out-of-sync/16566) in docker community forums.

I checked that the result of `date -u` and `curl http://s3.amazonaws.com -v` have different time in my docker container.

There are some solutions and what I like is [docker-time-sync-agent](https://github.com/arunvelsriram/docker-time-sync-agent/).

Reference:  
https://forums.docker.com/t/time-in-container-is-out-of-sync/16566  
https://github.com/arunvelsriram/docker-time-sync-agent
https://github.com/docker/for-mac/issues/17
