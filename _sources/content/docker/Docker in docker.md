# Docker in docker

`#docker` `#inside` `#dind` `#DooD` `#Nestybox` `#sysbox` `#runtime`

There are three ways to achieve docker in docker

1. Run docker by mounting `docker.sock` (DooD Method)
2. dind method
3. Using Nestybox sysbox Docker runtime

## Method 1: Docker in Docker Using [/var/run/docker.sock]

For example,

```bash
docker run -v /var/run/docker.sock:/var/run/docker.sock \
           -ti docker
```

If docker is rootless:

```docker
docker run -v $XDG_RUNTIME_DIR/docker.sock:/var/run/docker.sock \
           -ti docker
```

---

https://devopscube.com/run-docker-in-docker/