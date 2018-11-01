# Lab3 - Container Registry
The objective of this lab is to push the built image into a private registry with image scanning enabled.

* Login on registry
* Tag the container image
* Push the container image
* Check the vulnerability scanning
* Download an image from another delegate

## Login on registry
The lab is running a private registry, VMware Harbor. This is an open source registry and support integrations with other open source tools to bring more capabilities. This private registry is integrated with Clair, an open source image vulnerability scanning.

On your virtual machine run the following command to login. The username is *user* followed of your delegate number, i.e. **user1**

First you will need to know the IP address for the registry. Ping **reg.ntnxdemo.local** to get the IP address.

```shell
docker login <registry_IP>
```

For example:

```shell
docker login 10.10.56.188
```

You should get a *Login Succeeded* message.

## Tag the container image
Let's tag our container image with the path for the private registry. You need the container image ID or container image name as well as your email username.

To get the container image ID you can run:

```shell
docker image ls
```

To tag the container image as *version 1.0* with the new name:

```shell
docker tag <container_ID> <registry_IP>/library/<email username>/myfirstapp:1.0
```

For example:

```shell
docker tag d9c63af550b0 10.10.56.188/library/jose.gomez/myfirstapp:1.0
```

## Push the container image
Now we have the image properly tagged, let's push it into the private registry:

```shell
docker push <registry_IP>/library/<email username>/myfirstapp:1.0
```

For example:
```shell
docker push 10.10.56.188/library/jose.gomez/myfirstapp:1.0
```

You should get an output as follow:

```shell
The push refers to repository [10.10.56.188/library/jose.gomez/myfirstapp]
443e39316bc5: Pushed
86df2a1b653b: Pushed
bc5b41ec0cfa: Pushed
237472299760: Pushed
1.0: digest: sha256:d3464783884ebbdfa6a8bc40691ab45e200f01847ce4189ab41f09be7c316f37 size: 1155
```

## Check the vulnerability scanning
Open a web browser with the registry IP address (HTTP) and user the same credential you used to run the **docker login** command. It was user and your delegate number, i.e.: **user1**

Navigate to the library repository, your image, and click version 1.0. You should get a view of the current vulnerabilities on your image.

## Download an image from another delegate
From Harbor pick the name of any other image and pull this one on your virtual machine.

```shell
docker pull <registry_IP>/library/<delegate_image>
```

For example:

```shell
docker pull 10.10.56.188/library/jose.gomez/myfirstapp:1.0
```

You should get an output as follow:

```shell
1.0: Pulling from library/jose.gomez/myfirstapp
f17d81b4b692: Already exists
d5c237920c39: Already exists
a381f92f36de: Already exists
032083ca8813: Pull complete
Digest: sha256:d3464783884ebbdfa6a8bc40691ab45e200f01847ce4189ab41f09be7c316f37
Status: Downloaded newer image for 10.10.56.188/library/jose.gomez/myfirstapp:1.0
```

**Lab finished**