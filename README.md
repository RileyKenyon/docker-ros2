# Docker-ROS2
Repository for testing ROS2 code with docker

## Base image
Base layer is from the [Open Source Robotics Foundation (OSRF)](https://hub.docker.com/r/osrf/ros2/). OSRF also has images for amd64, arm64 and ROS 1 & 2 overlay images.

Dockerhub also has [ROS](https://hub.docker.com/_/ros/).

## Install docker dependencies
Docker dependencies to run the image
```
# Docker
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin

# docker-compose
sudo apt install docker-compose
```

### Cross Platform
From the docker docs
> You can build multi-platform images using three different strategies that are supported by Buildx and Dockerfiles:
>1. Using the QEMU emulation support in the kernel
>2. Building on multiple native nodes using the same builder instance
>3. Using a stage in Dockerfile to cross-compile to different architectures

The easiest is to install QEMU dependencies for cross-platform building (optional) See building multi-platform images for more information:
https://docs.docker.com/build/building/multi-platform/
```
docker run --privileged --rm tonistiigi/binfmt --install --all
```

## Push to container registry
An image may be tagged as from the container registry as "latest" using the syntax:
```
docker tag <image_name>:latest <github_container_registry>/<project_name>:<image_name>_<commit_hash>
```

Note when pushing to the registry it is best to practice to use the commit hash to avoid name conflicts. Easy way to get the latest hash is with 

```
git describe --abbrev=<num_characters>
```

We're able to use github workoflows to publish to the github container registry [ghcr.io](ghcr.io) - see the file `.github/workflows/deploy-image.yml` for details and [this guide](https://docs.github.com/en/packages/managing-github-packages-using-github-actions-workflows/publishing-and-installing-a-package-with-github-actions) for more information.

## Pulling from the container registry
To pull the image from the ghcr use the following syntax:
```
docker pull ghcr.io/rileykenyon/docker-ros2:v0.0.1
```
