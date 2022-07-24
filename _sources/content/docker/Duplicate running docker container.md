# duplicate running docker container

`#docker` `#duplicate` `#clone` `#copy` `#container` `#running`

You can create a new image from that container using the `docker commit` command:

```bash
docker commit c5a24953e383 new-image-name
```

And then start a new container from that image:

```bash
docker run [...same arguments as the other one...] new-image-name
```

---

[https://stackoverflow.com/questions/49193307/how-to-duplicate-running-docker-container](https://stackoverflow.com/questions/49193307/how-to-duplicate-running-docker-container)