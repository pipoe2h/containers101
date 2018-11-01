# Lab5 - Exploring Kubernetes
The objective of this lab is to get a basic knowledge about how to use the **kubectl** command-line to list the following Kubernetes objects:

* Nodes
* Namespaces
* Pods
* Services

For this lab you need to access to your virtual machine to run the *kubectl* commands.

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

## Namespaces
Like we have seen a Kubernetes namespace is just a logical grouping of Kubernetes objects in order to assign resources or have the chance to repeat object names across different namespaces.

To list the namespaces run the following command:

```shell
kubectl get ns
```

You should get an output as follow:

```shell
NAME           STATUS    AGE
default        Active    1d
kube-public    Active    1d
kube-system    Active    1d
ntnx-logging   Active    1d
```

By default the three firsts namespaces are created by Kubernetes during the installation process.

## Pods
Let's list the Pods for the *ntnx-logging* namespace.

```shell
kubectl -n ntnx-logging get pods
```

You can see we have running the pods for the EFK solution included in Karbon.

You can also describe pods with the same command we run it before for the node.

## Services
Let's check how we can access to our EFK stack getting the port for the service and the IP address of one of the workers.

To get the service details run the following command:

```shell
kubectl -n ntnx-logging get service
```

On the output you can see we have two services: ElasticSearch and Kibana. Let's get the port for Kibana which is *30950* on any of the worker nodes.

To get the workers IP address via *kubectl* you can run the following command:

```shell
kubectl get nodes -o json | grep address
```

Take the IP of one of the works, open a web browser, introduce the IP followed by the port and you should get the Kibana UI.

**Lab finished**
