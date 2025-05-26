# Introduction to Docker

## What is Docker?
A container platform that allows you to separate your application from the underlying infrastructure by bundling your code and all its dependencies to a self contained entity that will run the same on any supported system.

When it comes to software development, it's not the initial development that's challenging, it's everything that comes after that. Deploying code is a challenge, managing dependencies is a challenge, building rollbacks is a challenge, and all of these are made more challenging b/c development envs are seldom identical to production.

Docker containers are similar to their physical namesake. They allow you to take whatever software you need to run, bundle it up into a consistent format, and run it on any infrastructure that knows how to handle a container. The end result is like an executable for your code.

Can run apps on specific versions of containers. Having code run inside a container means is isolated from other processes and containers. Each container can have it's own process base, network stack, resource allocation, etc.

Docker containers are most often compared to virtual machines. They are completely different. Docker sits on top of VM, focuses more on application. Docker shares kernel w/ VM OS. 

---

## Docker Architecture
- Docker daemen responsible for managing Docker objects (e.g., images, containers).
- Daemen exposes REST API, the client consumes over Unix sockets or network interface.
- The client is the Docker binary. There is a separation between daemen and binary.
- Docker built on Linux kernal features.

Multiple technologies to create a complete Docker product.
- Namespaces allow you to isolate system resources.
    - pid - to handle process isolation.
    - net - used to handle IP stack.
    - ipc - to be isolated from other processes.
    - mnt - to handle file system isolation.
    - uts - to handle user and group isolation.

- Control groups (cgroups) allow you to limit resource allocation.
    - Resource limiting - CPU, memory, disk I/O, etc.
    - Prioritization - set priorities for processes.
    - Accounting - track resource usage.
    - Control - control resource allocation. Allow limits to be set on sub-systems.

UnionFS allows you to create a layered file system.
    - Merging - allows you to create a single file system from multiple layers.
    - Read/write - allows you to create a file system that can be modified.

Docker Architecture:
- Client-server
- Linux Kernel features
    - Namespaces
    - Cgroups
    - UnionFS

---

## Installing Docker
- Installing on CentOS linux.
TODO: Look at docs for running Docker on Windows.

---

## First Container
TODO: Look at Docker store for registration and images.
- Will pull down image from Marketplace if it doesn't exist locally.

### Summary
- Official Docker Registries
    - Docker Hub
    - Docker Store
- $ docker run
    - Downloads image
    - Runs the given command
- The flags 'i' and 't'
    - Create an interactive session (in container terminal)

## Images vs Containers

- Image (executable) - template that defines how the container will look once it creates an instance. Images built on concept of layers. Always a base layer, some number of additional layer that represents file changes. Each layer is stacked on top the others consisting between it and previous layer. The UFs is used to merge the differences.

- Container (running app) - own instance and independent of others, also separate from executable where changes to the app won't affect the executable.

---

## Images from the Dockerfile
Dockerfile is a text file with commands to create own image. Specify starting point and changes wish to be made to image. 

TODO: Get Docker code sheet.
Command to see current Docker images.
```
docker images
```

Dockerfile
    - FROM - image, begin with ones from the store.
    - COPY - copy files from host into layer of an image.
    - CMD - will be able to interact w/ binary in COPY. One CMD per Dockerfile. Multiple CMDs will tell Docker to exercise the last one.

Build container with Dockerfile based on where the file live.
```
docker build [directory w/ Dockerfile]
```

Remove a Docker image.
```
docker rmi [id]
```

Tags in Docker have own structure. Can provide repo name and tag at the same time.
```
docker build -t [name]
```

List all Docker containers.
```
docker ps -a
```

Remove a container.
```
docker container prune
```

List images.
```
docker images
```

---

## Images from a Container
Recommendation to commit images as part of a Dockerfile. Works as IaC for consistent reliability and sharing.

Use commit command to save images. Turn Container into an image.
```
docker commit [container id] [tag]
```

**Use official Python image for working with Python.**

Which Python to see what is currently installed on the Container.
```
which python
```

---

## Port Mapping
Docker runs in own network called Bridge Network. Each container has own IP address.

Can bind a port on container to the host. Publish All binds exposed port on the host. Test w/ a curl.
```
curl localhost:[port number]
```

Docker stop command.
```
docker stop [container id]
```

Can map to specific port on the host.
```
docker run -d -p [localhost port]:[container port]
```

---

## Networking
