# Build and Push Docker Images to Docker Hub

A quick guide to building a Docker image from a Dockerfile, tagging it, and pushing it to Docker Hub.

## 1. Log In to Docker Hub

```bash
docker version
docker login
```

> Sign up at [hub.docker.com](https://hub.docker.com/) first if you don't have an account.

## 2. Get the Source Code

```bash
mkdir demo-docker-build && cd demo-docker-build
wget https://github.com/aws-containers/retail-store-sample-app/archive/refs/tags/v1.2.4.zip
unzip v1.2.4.zip
```

## 3. Build the Image

```bash
cd retail-store-sample-app-1.2.4/src/ui

# Verify the Dockerfile exists
cat Dockerfile

# Build it
docker build -t retail-store-sample-ui:2.0.0 .

docker images
```

## 4. Run and Test the Image

```bash
docker run --name myapp1-v2 -p 8889:8080 -d retail-store-sample-ui:2.0.0
```

Visit `http://<EC2-Instance-Public-IP>:8889` to check it.

## 5. Tag the Image

```bash
docker tag retail-store-sample-ui:2.0.0 YOUR_DOCKER_USERNAME/retail-store-sample-ui:2.0.0
```

## 6. Push to Docker Hub

```bash
docker push YOUR_DOCKER_USERNAME/retail-store-sample-ui:2.0.0
```

## 7. Verify

Log in to [Docker Hub](https://hub.docker.com/repositories) and check your repositories to confirm the image was pushed.

## Notes

- Replace `YOUR_DOCKER_USERNAME`, container names, ports, and tags with your own values.
- Free Docker Hub accounts get unlimited public repos; private repos may need a paid plan.
- `docker system prune` clears unused images/containers — use with caution, it removes everything unused.

## Resources

- [Docker Docs](https://docs.docker.com/)
- [Docker Hub Quickstart](https://docs.docker.com/docker-hub/)
- [Dockerfile Best Practices](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/)
