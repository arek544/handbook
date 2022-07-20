# Docker build

#docker #build

Docker `build` creates Docker images from [Dockerfiles](https://docs.docker.com/engine/reference/builder/).

You can easily build a new image from a Dockerfile and tag it with:

```bash
docker build <PATH> -f <DOCKERFILE> -t <NAME>:<TAG>
```

Example:

```bash
docker build -f docker/Dockefile -t my-rails-app:latest .
```

- `f` specifies the path to the actual Dockerfile,
- `PATH` (`.` in the example) tells Docker what to use for its context or current directory when building the image. (This is important when considering commands specifying files and paths within the Dockerfile.)
- `t` will tag the image built by Docker.

> All Docker images have an image identifier (a generated, 12-character alphanumeric string). They may also be given a name and a tag. If only a name is provided, the default tag of “latest” is used. Image names and tags help tremendously to readily (and unambiguously) reference specific images.

