# docker-compose for detached mode

#docker #compose #detached #background #interactive #stdin #tty

you have to use `tty: true` and `stdin_open: true`. Here is a minimal example:

```yaml
version: "3"
services:
  alpine1:
    image: alpine
    tty: true
    stdin_open: true

```

Start with:

```bash
docker-compose up -d
```

or

```bash
docker-compose up --detach
```