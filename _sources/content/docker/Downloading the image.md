# Downloading the image

`#docker` `#image` `#download` `#pull`

## Downloading the image 
(from DockerHub by default)

```bash
docker pull image-name
```

## Example

Image is provided by the [Jupyter project](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html). Jupyter Notebook Python, Spark, Mesos Stack from https://github.com/jupyter/docker-stacks

```bash
docker pull jupyter/pyspark-notebook
```

If you need to find Docker images available locally, you can run:

```bash
docker images
```

or 

```bash
docker image ls
```

