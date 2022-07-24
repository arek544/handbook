#docker #rootless #root #user 

# Docker-rootless

# Root user

```bash
sudo apt install curl
sudo apt install uidmap
```

# Non-root user

Launch the installation script :

```bash
curl -sSL https://get.docker.com/rootless | sh
```

You need to specify the socket path and the CLI context explicitly.

In your `~/.bashrc` file, add these three lines to specify the socket path using `$DOCKER_HOST`:

```bash
export PATH=/home/$(whoami)/bin:$PATH
export DOCKER_HOST=unix:///run/user/$(id -u)/docker.sock
```

> Warning! docker in rootless mode so the docker.sock file is in $XDG_RUNTIME_DIR/docker.sock, consider this in case of docker-in-docker aplication (Docker in docker)
> 

To specify the CLI context using `docker context`:
```bash
docker context use rootless
```

Start the Docker daemon with this command :

```bash
systemctl --user start docker
```


# Root user

To launch the daemon on system startup, enable the systemd service and lingering :

```bash
systemctl --user enable docker
sudo loginctl enable-linger <user name>
```

---

https://medium.com/@flavienb/installing-and-securing-docker-rootless-for-production-use-8e358d1c0956

https://stackoverflow.com/questions/71322556/rootless-docker-remote-system-and-vs-code-attach-vs-code-to-container-failin

https://docs.docker.com/engine/security/rootless/
