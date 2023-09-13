# 1. Creating and Running Containers

**_Contianer images are constructed with a series of filesystem layers where each layer inherits and modifies the layers that came before it_**

## Dockerfile Basics

```
1. FROM node:16

2. WORKDIR /usr/src/app

3. COPY package*.json ./
   RUN npm install
   RUN npm install express

4. COPY . .

5. CMD ["npm", "start"]
```

_Assume a basic NodeJS project_

1. Specifies the image starts with `node:16` the image
2. Set the working directory to be `/app`
3. Copys over `package.json` and `package.lock.json` into `/app` and then install the dependencies (`node_modules`, etc)
4. Copy everything (except the `node_module` which can be done via `.dockerignore` file)
5. Run the program

To create a new docker image called `node-project`

- `docker build -t node-project .`

To make a container from the image and allow `http://localhost:3000` access

- `docker run --rm -p 3000:3000 node-project`

_These steps build an image accessible to the local Docker registry_

### Notes

If a layer in an image has a _big file_ in layer 1 and layer 2 removes it, when the image is transmitted through the network, _big file_ will be transmitted as well while still being inaccessible

Changing a preceding layer means that all proceeding layers will need to be rebuilt, repushed, and repulled to deploy

Don't build containers with passwords backed in

Secrets and images should never be mixed

Minimize the files within the container image

## Multistage Image Builds

**_Producing multiple images to prevent building large images_**

Each image is consideered a stage and artifacts can be copied from preceding stages to the current stage

```dockerfile
# STAGE 1: Build
FROM golang:1.17-alpine AS build

# Install Node and NPM
RUN apk update && apk upgrade && apk add --no-cache git nodejs
bash npm

# Get dependencies for Go part of build
RUN go get -u github.com/jteeuwen/go-bindata/...
RUN go get github.com/tools/godep
WORKDIR /go/src/github.com/kubernetes-up-and-running/kuard

# Copy all sources in
COPY . .

# This is a set of variables that the build script expects
ENV VERBOSE=0
ENV PKG=github.com/kubernetes-up-and-running/kuard
ENV ARCH=amd64
ENV VERSION=test

# Do the build. Script is part of incoming sources.
RUN build/build.sh

# STAGE 2: Deployment
FROM alpine

USER nobody:nobody
COPY --from=build /go/bin/kuard /kuard

CMD [ "/kuard" ]
```

First build image contains Go compiler, ReactJS toolchain, and the program source code

Second build image only contains the compiled binary

**Build**: `docker build -t kuard .`

**Run**: `docker run --rm -p 8080:8080 kuard`

### Storing Images in a Remote Registry

**_Images can now be reused by multiple authorized machines_**

Upload to public registries to share with the world and private to keep them to yourself

Authentication is required to push an image (public or private) which can be done via `docker login` (varies on registry provider)

Tag the image by prepending it to the target registry

- `docker tag kuard target_registry`

Push the image

- `docker push target_registry`

## The Container Runtime Interface

**_A stander defining how Kubernetes sets up and application container using the container-specific APIs native to the target OS_**

Kubernetes containers are lauched by a daemon on each node called _kubelet_

Depolying a container from `target_registry`

- `docker run -d --name kuard -p 8080:8080 target_registry`
  - starts `kurad` container
  - maps ports 8080 on local machine to 8080 in the container (`-p`)
  - runs in the background (`-d`)

## Options to Note

`docker run -d --name kuard -p 8080:8080 --memory 200m --memory-swap 1G --cpu-shares 1024`

- Limits the image to 200MB of memory
- Limits the image to 1Gb of swap space
- Limits CPU utilization

Image build will fail if build exceeds these settings

Delete image after building them

- `docker rmi <tag-name>`
- `docker rmi <image-id>`
