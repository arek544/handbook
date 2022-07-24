# Multi-stage build

`#build` `#docker` `#compose` `#stage` `#multi`

- multi-stage build involves a single Dockerfile to perform multiple stages

You could convert these to a non-traditional multi-stage build with a syntax like (I say non-traditional because you do not perform any copying between the layers and instead use just the from line to pick from a prior stage):

```dockerfile
FROM python:3.6 as base
RUN apt-get update && apt-get upgrade -y
RUN pip install pipenv pip
COPY Pipfile ./
# some more common configuration...

FROM base as dev
RUN pipenv install --system --skip-lock --dev
ENV FLASK_ENV development
ENV FLASK_DEBUG 1

FROM base as prod
RUN pipenv install --system --skip-lock
ENV FLASK_ENV production

```

Then you can build one stage or another using the `--target` syntax to build, or a compose file like:

```yaml
version: '3.4'
services:
  webapp:
    build:
      context: ./dir
      dockerfile: Dockerfile
      target: prod

```

The biggest downside is the current build engine will go through every stage until it reaches the target. Build caching can mean that's only a sub-second process. And BuildKit which is coming out of experimental in 18.09 and will need upstream support from docker-compose will be more intelligent about only running the needed commands to get your desired target built.

All that said, I believe this is trying to fit a square peg in a round hole. The docker-compose developer is encouraging users to move away from doing the build within the compose file itself since it's not supported in swarm mode. Instead, the recommended solution is to perform builds with a CI/CD build server, and push those images to a registry. Then you can run the same compose file with `docker-compose` or `docker stack deploy` or even some k8s equivalents, without needing to redesign your workflow.