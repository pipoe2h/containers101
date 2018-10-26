# Lab1 - Container Image
The objective of this lab is to show you the common tasks around container image operations.

* Pull
* Inspect
* History
* Builld
* Tag

## Pull an image
Let's pull the Ubuntu 15.04 image you saw in the slide and explore the layers.
```shell
docker pull ubuntu:15.04
```
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

```shell
docker image inspect ubuntu:15.04
```

## History

```shell
docker image history ubuntu:15.04
```

## Build

```shell
docker build .
```

## Tag