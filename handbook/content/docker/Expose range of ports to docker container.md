# Expose many ports to docker container

`#docker` `#port` `#expose`

You can expose a range of ports using the `-p` option, for example:

```docker
docker run -p 2000-5000:2000-5000 -v /host/:/host appimage
```

---

https://stackoverflow.com/questions/33695203/how-to-forward-all-ports-in-docker-container