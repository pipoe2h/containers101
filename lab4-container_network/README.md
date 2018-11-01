# Lab4 - Container Network
The objective of this lab is to create a new network and connect an instance of our web application listening on port *8080*.

* Create container network
* Create container connected to the new network
* Inspect the new network
* Test the application access

## Create container network
To create a new container network run the following command:

```shell
docker network create bootcamp
```

List the networks and check the new one has been created.

```shell
docker network ls
```

You should get an output as follow:

```shell
NETWORK ID          NAME                DRIVER              SCOPE
09520e45cae3        bootcamp            bridge              local
eeb13cb1c5bd        bridge              bridge              local
b5bcf0246d96        host                host                local
a0e6b14041a8        none                null                local
```

## Create container connected to the new network
Let's create a container with the image we downloaded from the private registry, another delegate image, and connect it to the new network.

```shell
docker container run -d --rm --name mycolleageapp --network bootcamp -p 8080:80 <delegate_container_image>
```

For example:

```shell
docker container run -d --rm --name myfirstapp -p 8080:80 --network bootcamp 10.10.56.188/library/jose.gomez/myfirstapp:1.0
```

## Inspect the new network
Let's check the new container is connected to the bootcamp network

```shell
docker network inspect bootcamp
```

If you look through the metadata you will see the container has been connected and an IP has been assigned too.

## Test the application access
Open a web browser and using your virtual machine IP address and port *8080* check the website is up and running.

**Lab finished**