`#docker` `#save` `#load` `#push` `#pull` 

You will need to save the Docker image as a tar file:

```
docker save -o <path for generated tar file> <image name>
```

Then copy your image to a new system with regular file transfer tools such as `cp`, `scp` or `rsync`(preferred for big files). After that you will have to load the image into Docker:

```
docker load -i <path to image tar file>
```

PS: You may need to `sudo` all commands.

EDIT: You should add filename (not just directory) with -o, for example:

```
docker save -o c:/myfile.tar centos:16
```


https://stackoverflow.com/questions/23935141/how-to-copy-docker-images-from-one-host-to-another-without-using-a-repository