# Volumes - Persistent Data in Containers
#docker #volume #mapping 

- independent from containers
- mapped to external storage
- multiple container can access same volume

>Voliums are managed very similarly to images and containers, the commands are analogous

- create volume 
```bash
docker volume create [OPTIONS] my-volume-name
```

## 3 types of  volumes

- host-mounted volume (volumes sheared between host machine and container)
```bash
docker run -v /host-folder:/container-folder my-container-name
```

**Equivalent `--mount`**
```bash
docker run --mount source=/host-folder,target=/container-folder my-container-name
```

- anonymous volume
```bash
docker run -v /container-folder my-container-name
```
Docker automatically creates mounting folder (`/var/lib/docker/volumes/random-hash/_data`)
- named volume (volumes sheared between a other containers)
```bash
docker run -v name:/container-folder my-container-name
```

## Docker-compose 

```yaml
version: "3.9" # version fo compose file format

volumes:
    my-volume:
        name: my-volume
        external: true

services: # all services
    my-service: # name of single service
        container_name: my-container-name
        image: my-image-name
        build:
            context: . # where to look for Dockerfile
            dockerfile: Dockerfile # Dockerfile name
            target: prod # specification for multi-stage Dockerfile
        stdin_open: true # to allow detached mode
        tty: true # to allow detached mode
        volumes: 
            - ./host-dir:/dir-in-container # volume mapping
            - my-volume:/dir-in-container # named volume
            - /dir-in-container # anonymous volume
        network_mode: host # use host network
        ports: 
            - 80:80 
    another-service: 
        image: python # image from DockerHub 
        depends_on: my-service # this container not going to work unless my-service is running
```

## Internal vs External volume

- internal named volumes have the scope of a single Docker-compose file and Docker creates them if they don’t exist
- external named volumes can be used across the Docker installation and they need to be created by the user (otherwise fails) using the _docker volume create_ command.

## Sharing volumes
We can start a new container using volumes defined in another.
```bash
docker run -it --name my-container --volumes-from another-container my-image:my-tag 
```

https://docs.docker.com/storage/volumes/
https://devopsheaven.com/docker/docker-compose/volumes/2018/01/16/volumes-in-docker-compose.html