# DockerHub

`#DockerHub` `#explained` `#push` `#pull` `#docker`

![Untitled](ATTACHMENTS/Untitled.png)

- repository of Docker images provided by the community similar to GitHub repositories
- you can store images (1 image for free)
- you can pull and rebuild the given environment

# Pull

- by default, the Docker CLI uses DockerHub, you can use `docker pull image-name` to download a given image from DockerHub

![Untitled](ATTACHMENTS/Untitled-1.png)

# **Deploy containers (push)**

```bash
docker login
docker push image-name
```

> ## Remark
> the images to be pushed must be named after the repository
> ```
> repo-name/image-name
> ```
> To rename (or tag) existing containers use following command:
> ```
> docker tag old-name new-name
> ```

# Alternative repositories:
- GitLab Container Registry
- Google Container Registry (GCR.io)
- IBM Cloud Container Registry
- Azure Container Registry