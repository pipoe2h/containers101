# Lab1 - Container Image
The objective of this lab is to show you what are the common tasks to manage container images.

* Pull
* Inspect
* History
* Build
* Tag

## Pull an image
Let's pull the Ubuntu 15.04 image you saw in the slide and explore the layers.

```shell
docker pull ubuntu:15.04
```

You should get an output as follow:

```shell
15.04: Pulling from library/ubuntu
9502adfba7f1: Pull complete
4332ffb06e4b: Pull complete
2f937cc07b5f: Pull complete
a3ed95caeb02: Pull complete
Digest: sha256:2fb27e433b3ecccea2a14e794875b086711f5d49953ef173d8a03e8707f1510f
Status: Downloaded newer image for ubuntu:15.04
```

## Inspect
With this command you get the metadata information for the container image.

```shell
docker image inspect ubuntu:15.04
```

## History
With this command you can list the layers for the container image.

```shell
docker image history ubuntu:15.04
```

## Build
With this command you build new versions of your container image which includes the application too.

We are going to build a container image with Nginx and a simple HTML page.

1. Move to the lab directory

```shell
cd ~/containers101/lab1-container_image/
```

2. Have a look to the existing Dockerfile

```shell
cat Dockerfile
```

3. Edit the Dockerfile and modify the maintainer with your email address

```shell
nano Dockerfile
```

Use CTRL+X to save, followed of Y (yes), and press ENTER.

4. Let's build the container image

```shell
docker build . 
```

You should get an output as follow:

```shell
Sending build context to Docker daemon  8.704kB
Step 1/3 : FROM nginx
latest: Pulling from library/nginx
f17d81b4b692: Pull complete
d5c237920c39: Pull complete
a381f92f36de: Pull complete
Digest: sha256:b73f527d86e3461fd652f62cf47e7b375196063bbbd503e853af5be16597cb2e
Status: Downloaded newer image for nginx:latest
 ---> dbfc48660aeb
Step 2/3 : LABEL maintainer="jose.gomez@nutanix.com"
 ---> Running in 1d62f0af33d7
Removing intermediate container 1d62f0af33d7
 ---> a901e00a01c9
Step 3/3 : COPY html /usr/share/nginx/html
 ---> adc5195c1e62
Successfully built adc5195c1e62
 ```

5. List what images are available after the build

```shell
docker image ls
```

You should get a similar output as follow:

```shell
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
<none>                    <none>              c9de1af1ca97        2 minutes ago       109MB
pipoe2h/rancheros-nano    latest              2223c96442fb        5 days ago          12.1MB
nginx                     latest              dbfc48660aeb        12 days ago         109MB
bwits/docker-git-alpine   latest              c85b15cccb41        17 months ago       27.8MB
```

The one at the top is the container image you just built. You can see the image doesn't have a name or tag yet.

Write down the *IMAGE ID* for the container image you just created. You will need it for the next section.

## Tag
Tags help to identify the container image with a name as well as the version of your image. **Note: for production the use of tag latest is not recommended**

1. Let's tag our container image with a name and tag *latest*. The name will be your email address without the domain part (i.e.: *jose.gomez*) 

```shell
docker tag <IMAGE ID> <email.user>/myfirstapp:<tag> 
```

For example:

```shell
docker tag c9de1af1ca97 jose.gomez/myfirstapp:latest
```

To check the tagging went good, you can list the images:

```shell
docker image ls
```

You should get a similar output as follow:
```shell
REPOSITORY                TAG                 IMAGE ID            CREATED             SIZE
jose.gomez/myfirstapp     latest              c9de1af1ca97        23 minutes ago      109MB
pipoe2h/rancheros-nano    latest              2223c96442fb        6 days ago          12.1MB
nginx                     latest              dbfc48660aeb        12 days ago         109MB
bwits/docker-git-alpine   latest              c85b15cccb41        17 months ago       27.8MB
```

# Test
We will look later in depth how to run containers, but for the purpose of this exercise we will test our image works.

Run the following command:

```shell
docker run -d --name myfirstapp -p 8080:80 <container_image>
```

For example:

```shell
docker run -d --name myfirstapp -p 8080:80 jose.gomez/myfirstapp
```

To confirm the application is running and exposed in your virtual machine, open a web browser and type the IP address of your virtual machine followed of port *8080*, i.e. http://10.10.56.184:8080

**Lab finished**