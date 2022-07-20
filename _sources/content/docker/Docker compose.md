# Docker compose

#docker #compose #run #yaml #example #DockerCompose #detached #background #interactive #stdin #tty #yml

- extends the capabilities of the `docker run` command 
- lets us define all services (multi-container Docker applications) in a **one configuration file**
- startup all services with a **single command**
- works in **all environments**: production, staging, development, testing, as well as CI workflows.

# Example `docker-compose.yaml` file:

```dockerfile
version: "3.9" # version fo compose file format

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
        volumes: # volume mapping
            - "./host-dir:/dir-in-container"
        network_mode: "host" # use host network
		ports: 
			- 80:80 
	another-service: 
		image: python # image from DockerHub 
		depends_on: my-service # this container not going to work unless my-service is running
```

To run this use the following command:

```bash
docker-compose up
```
or 
```bash
docker compose up
```

Run in background:

```bash
docker-compose up --detach
```
or in short:

```bash
docker-compose up -d
```
# Standard workflow

1. Define your app’s environment with a `Dockerfile` .
2. Define the services that make up your app in `docker-compose.yaml` so they can be run together in an isolated environment.
3. Run `docker-compose up` and the [Docker compose command](https://docs.docker.com/compose/cli-command/) starts and runs your entire app. 

---
https://towardsdatascience.com/dockerizing-jupyter-projects-39aad547484a