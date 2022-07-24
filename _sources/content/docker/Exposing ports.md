# Exposing ports

`#docker` `#dockerfile` `#expose` `#port` `#host` `#network` 

In `Dockerfile` we use line:

```bash
EXPOSE 80
```

to expose port 80 as an example. 

This means the container will be listening on port 80, by default other ports will be ignored.

Then while running the container you will have to use option `-p` as shown below:

```bash
docker run -p 80:80 my-container-name
```

This means that port 80 on your machine is forwarded to container port 80.

```bash
-p host-machine-port:container-port
```