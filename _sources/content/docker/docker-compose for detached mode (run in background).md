# docker-compose for detached mode

#docker #compose #detached #background #interactive #stdin #tty

you have to use `tty: true` and `stdin_open: true`. Here is a minimal example:

```docker
version: "3"
services:
  alpine1:
    image: alpine
    tty: true
    stdin_open: true

```

Start with:

```
docker-compose up -d
```

or

```docker
docker-compose up --detach
```