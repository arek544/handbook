# Update given container/service via docker-compose

`#docker` `#update` `#container` `#service` `#build` `#force` `#rebuild` `#recreate`

```bash
docker-compose up -d
```

To restart only one container you can simply do:

```bash
docker-compose up -d --build image-name
```

if container is dependent on others:

```docker
docker-compose up --force-recreate --no-deps service-name
```

---

[https://stackoverflow.com/questions/50947938/docker-compose-orphan-containers-warning](https://stackoverflow.com/questions/50947938/docker-compose-orphan-containers-warning)

[https://stackoverflow.com/questions/49316462/how-to-update-existing-images-with-docker-compose](https://stackoverflow.com/questions/49316462/how-to-update-existing-images-with-docker-compose)

[https://stackoverflow.com/questions/38086453/docker-compose-for-detached-mode](https://stackoverflow.com/questions/38086453/docker-compose-for-detached-mode)

[https://stackoverflow.com/questions/47081505/docker-compose-force-recreate-specific-service](https://stackoverflow.com/questions/47081505/docker-compose-force-recreate-specific-service)