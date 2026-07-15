# Pull and Run Docker Images from Docker Hub

A quick guide to pulling images, running containers, and managing them with basic Docker CLI commands.

## 1. Pull an Image

```bash
docker images
docker pull stacksimplify/retail-store-sample-ui:1.0.0
docker images
```

> Hitting Docker Hub rate limits? Pull from GitHub Packages instead:
> `docker pull ghcr.io/stacksimplify/retail-store-sample-ui:1.0.0`

## 2. Run a Container

```bash
docker run --name myapp1 -p 8888:8080 -d stacksimplify/retail-store-sample-ui:1.0.0
```

- `-p HOST_PORT:CONTAINER_PORT` maps the container's port to your host
- `-d` runs it in the background

Visit `http://<EC2-Instance-Public-IP>:8888/` in your browser.

## 3. List Containers

```bash
docker ps        # running only
docker ps -a      # all, including stopped
```

## 4. Access a Container's Shell

```bash
docker exec -it myapp1 /bin/sh
```

Useful commands once inside:

```bash
whoami
ls /app
curl http://localhost:8080
exit
```

## 5. Stop and Start a Container

```bash
docker stop myapp1
docker start myapp1
```

## 6. Remove a Container

```bash
docker rm -f myapp1
```

## 7. Remove an Image

```bash
docker rmi stacksimplify/retail-store-sample-ui:1.0.0
```

## Notes

- Replace `myapp1`, ports, and image names with your own values.
- Clean up unused containers/images regularly to save disk space.

## Resources

- [Docker Docs](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [GitHub Container Registry](https://docs.github.com/en/packages/working-with-a-github-packages-registry/working-with-the-container-registry)
