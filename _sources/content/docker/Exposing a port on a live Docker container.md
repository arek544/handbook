# Exposing a port on a live Docker container

`#docker` `#port` `#ip` `#expose` `#network` 

You cannot do this via Docker, but you can access the container’s un-exposed port from the host machine.

If you have a container with something running on its port 8000, you can run

```bash
wget http://container_ip:8000
```

To get the container’s IP address, run the 2 commands:

```bash
docker ps
docker inspect container_name | grep IPAddress
```

Internally, Docker shells out to call IP tables when you run an image, so maybe some variation on this will work.

To expose the container’s port 8000 on your localhost’s port 8001:

```bash
iptables -t nat -A  DOCKER -p tcp --dport 8001 -j DNAT --to-destination 172.17.0.19:8000
```

One way you can work this out is to setup another container with the port mapping you want, and compare the output of the **iptables-save** command (though, I had to remove some of the other options that force traffic to go via the docker proxy).

**NOTE: this is subverting docker, so should be done with the awareness that it may well create blue smoke.**

OR

Another alternative is to look at the (new? post 0.6.6?) -P option - which will use random host ports, and then wire those up.

OR

With 0.6.5, you could use the LINKs feature to bring up a new container that talks to the existing one, with some additional relaying to that container’s -p flags? (I have not used LINKs yet.)

OR

With docker 0.11? you can use `docker run --net host ..` to attach your container directly to the host’s network interfaces (i.e., net is not namespaced) and thus **all** ports you open in the container are exposed.

[Exposing a port on a live Docker container - Stack Overflow](https://stackoverflow.com/questions/19897743/exposing-a-port-on-a-live-docker-container)