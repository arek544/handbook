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

Now, to be able to use the Docker CLI for your daemon, you need to export some parameters. In your `~/.bashrc` file, add these three lines :

```bash
export PATH=$PATH:/sbin
export DOCKER_HOST=unix:///run/user/$(id -u)/docker.sock
```

> Warning! docker in rootless mode so the docker.sock file is in $XDG_RUNTIME_DIR/docker.sock, consider this in case of docker-in-docker aplication (Docker in docker)
> 

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

[https://pastebin.com/Ay64dj3b](https://pastebin.com/Ay64dj3b)

Ustawiamy domyślne dla jsona

W VSC F1 → Settings (JSON) → “files.associations”:  {”*.json”: “jsonc”}

[https://tiny.pl/92xdd](https://tiny.pl/92xdd)

Hasło: 

host_saventic