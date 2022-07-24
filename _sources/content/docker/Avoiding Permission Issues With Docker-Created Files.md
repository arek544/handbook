# Avoiding Permission Issues With Docker-Created Files

`#docker` `#permission` `#create` `#file` `#ownership` `#owner` 

## Issue:

- The **user of the container** (root in the worst case) is completely **different than the one on the host**.
- The file **permissions and ownership are all wrong**.

## Solutions

### The “chown” method

One frequent solution, is to “chown” your shared folder again and again.

### Example

Taking ownership of the files from your shared folder can be done with `chown`. Here is a simple example of creating a new file with wrong permissions:

```bash
$ docker run -it --rm \
	--mount "type=bind,src=$(pwd)/shared,dst=/opt/shared" \
	--workdir /opt/shared \
	ubuntu bash

# now we're root in the new container:
$ touch newfile
```


> **NOTE:** 
> if you’re using something like docker on mac, you won’t run into those permission issues, as the file-sharing is done through NFS and your local files will have the right user.

We work on the `shared` folder and create a file `newfile` from within a temporary container. As the container ran with the “root” user by default, we won’t be able to use those files from the host. One way to fix them temporarily is to take ownership of them again and again and again:

```bash
$ chown -R hostuser:hostuser shared
...
$ chown -R hostuser:hostuser shared
...
$ chown -R hostuser:hostuser shared
```

If you want to write shared data from within your Docker container and use it from your host regularly, this can get tedious really fast. In addition, this approach can break the dockerized program for future runs, especially if the container’s user does not have root permissions.

You can do better.

## Set the Docker user when running your container

You can run the ubuntu image with an explicit user id and group id.

```bash
$ docker run -it --rm \
	--mount "type=bind,src=$(pwd)/shared,dst=/opt/shared" \
	--workdir /opt/shared \
	--user "$(id -u):$(id -g)" \
	ubuntu bash
```

The difference is ‘–user “(*id* − *u*):(id -g)“’ - they tell the container to run with the current user id and group id which are obtained dynamically through bash command substitution by running the “id -u” and “id -g” and passing on their values.

This can be good enough already. The problem here is, that the user and group don’t really exist in the container. This approach works for the terminal command, but the session looks broken and you’ll see some ugly error messages like:

```
"groups: cannot find a name for group ID"
"I have no name!"
  - your container, complaining
```

While bash works, some apps might refuse to run if those configs look fishy.

## Build the right image

Now it gets more interesting. Here is how you can build, configure and run your Docker containers correctly, so you don’t have to fight permission errors and access your files easily.

As you should create a non-root user in your Dockerfile in any case, this is a nice thing to do. While we’re at it, we might as well set the user id and group id explicitly.

Here is a minimal Dockerfile which expects to receive build-time arguments, and creates a new user called “user”:

```dockerfile
FROM ubuntu

ARG USER_ID
ARG GROUP_ID

RUN addgroup --gid $GROUP_ID user
RUN adduser --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID user
USER user
```

(check out [https://stackoverflow.com/questions/27701930/add-user-to-docker-container](https://stackoverflow.com/questions/27701930/add-user-to-docker-container) for more info on adduser)

We can use this Dockerfile, to build a fresh image with the host uid and gid. This image, needs to be built specifically for each machine it will run on to make sure everything is in order.

Then, we can run use this image for our command. The user id and group id are correct without having to specify them when running the container.

```bash
$ docker build -t myimage \
	--build-arg USER_ID=$(id -u) \
	--build-arg GROUP_ID=$(id -g) .
$ docker run -it --rm \
	--mount "type=bind,src=$(pwd)/shared,dst=/opt/shared" \
	--workdir /opt/shared \
	myimage bash
```

No need to use “chown”, and no annoying permission errors anymore!

---

https://vsupalov.com/docker-shared-permissions/