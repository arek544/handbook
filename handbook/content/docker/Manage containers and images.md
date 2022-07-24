# Manage containers

`#docker` `#container` `#volume` `#kill` `#close` `#remove` `#prune` `#tag` `#inspect` `#ls` `#list` `#manage` `#delete` `#stop` `#remove` `#delete`


## `docker container` allows you to manage containers, for example:

- list all running containers
	```bash
	docker container ls
	```
- start container
	```bash
	docker start <container-id/name>
	```
- stop container  
	```bash
	docker stop <container-id/name>
	```
- forcefully stop a running container
	```bash
	docker container kill CONTAINER-NAME-OR-ID
	``` 
- remove a container
	```bash
	docker container rm CONTAINER-NAME-OR-ID
	```  
- view detailed information about a running container
	```bash
	docker inspect CONTAINER-NAME-OR-ID
	``` 
- pause container
	```bash
	docker pause <container-id/name>
	```
- unpause container  
	```bash
	docker unpause <container-id/name>
	```
- restart container  
	```bash
	docker restart <container-id/name>
	```

## `docker images` allows you to manage images, for example:

- list all locally available images
	```bash
	docker image ls
	```
- remove an image
	```bash
	docker image rm IMAGE-NAME
	```
- to remove dangling images (those not attached to a container, or a dependency for an image that is)
	```bash
	docker image prune
	```
- to remove all images
	```bash
	docker image prune -a
	``` 
- tag an image from one image id or tag, to a new tag. (e.g. `my-app:latest` to `my-app:1.0.0`)
	```bash
	docker image tag OLD-IMAGE-NAME NEW-IMAGE-NAME
	```


---

https://spin.atomicobject.com/2018/10/04/docker-command-line/