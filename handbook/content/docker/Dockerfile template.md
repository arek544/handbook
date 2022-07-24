# Dockerfile template

`#docker` `#DockerFile` `#DataScience` `#template` `#setup` `#CodeSnippet`

## Container for python data science project

`Dockerfile`

```dockerfile
FROM python:3.8.7

# creating an environment variable that holds the project directory
ENV PYTHONPATH="/workspace"
WORKDIR "${PYTHONPATH}"

# install python dependencies
RUN pip install pipenv
COPY requirements.txt .
RUN pip install -r requirements.txt 

CMD ["jupyter", "lab", "--no-browser", "--allow-root"]
```

Script to create and start the container:

```bash
export NAME="data-science-playground"
docker build -t $NAME -f Dockerfile .
docker stop $NAME
docker rm $NAME
docker run -it -p 8888-9000:8888-9000 -v $PWD:/workspace --name=$NAME $NAME
```

or use following `docker-compose.yaml` instead:

```yaml
version: "3.9" # version fo compose file format

services: # all services
    data-science-playground: # name of single service
        container_name: data-science-playground
        image: data-science-playground
        build:
            context: . # where to look for Dockerfile
            dockerfile: Dockerfile # Dockerfile name
        stdin_open: true # to allow detached mode
        tty: true # to allow detached mode
        volumes: # volume mapping
            - ".:/workspace"
        network_mode: "host" # use host network
```

```
docker-compose up
```