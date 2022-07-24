# Kill container from inside

`#kill` `#remove` `#container` `#docker` `#stop` `#prune`

```bash
host$ docker exec -it <container-name> sh
container$ ps
PID   USER     TIME  COMMAND
    1 root      0:00 {entrypoint.sh} /bin/sh /entrypoint.sh
   16 root      0:00 {entrypoint.sh} /bin/sh /entrypoint.sh
   24 root      0:00 sh
   31 root      0:00 ps
container$ kill 1
```