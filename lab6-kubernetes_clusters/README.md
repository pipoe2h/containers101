# Lab6 - Kubernetes Clusters
The objective of this lab is to get a basic knowledge about how to use the **kubectl** command-line to list the following Kubernetes objects:

* Cluster info
* Nodes

For this lab you need to access to your virtual machine to run the *kubectl* commands.

## Cluster info
Typically, there are several services which are started on a cluster by kube-system. Get a list of these with the kubectl cluster-info command:

```shell
kubectl cluster-info
```

Kubectl handles locating and authenticating to the apiserver. If you want to directly access the REST API with an http client like curl or wget, or a browser, there are several ways to locate and authenticate. We are going to use the easiest and recommended approach, this is using *kubectl* in proxy mode.

```shell
kubectl proxy --port=8080
```

Then you can explore the API with curl, wget, or a browser, replacing localhost with [::1] for IPv6, like so:

```shell
curl http://localhost:8080/api/
```

## Nodes
Let's list the Kubernetes nodes on our Karbon cluster.

```shell
kubectl get nodes
```

You can see we have a single master and two workers.

To get more details about one of the nodes we can run the following command similar to inspect on Dockers.

```shell
kubectl describe node k8s-9397b5-k8s-master-0
```

You will get details like resources, uptime and so on.

**Lab finished**