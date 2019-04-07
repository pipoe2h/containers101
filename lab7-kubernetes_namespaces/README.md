# Lab7 - Kubernetes Namespaces
The objective of this lab is to get a basic knowledge about how to use Kubernetes Namespaces.

For this lab you need to access to your virtual machine to run the *kubectl* commands.

## Namespaces
Like we have seen a Kubernetes namespace is just a logical grouping of Kubernetes objects in order to assign resources or have the chance to repeat object names across different namespaces.

To list the namespaces run the following command:

```shell
kubectl get namespaces
```

You should get an output similar as follow:

```shell
NAME           STATUS    AGE
default        Active    1d
kube-public    Active    1d
kube-system    Active    1d
monitoring     Active    1d
ntnx-logging   Active    1d
```

By default the three firsts namespaces are created by Kubernetes during the installation process.

For this exercise, we will create two additional Kubernetes namespaces to hold our content.

Let’s imagine a scenario where an organization is using a shared Kubernetes cluster for development and production use cases.

The development team would like to maintain a space in the cluster where they can get a view on the list of Pods, Services, and Deployments they use to build and run their application. In this space, Kubernetes resources come and go, and the restrictions on who can or cannot modify resources are relaxed to enable agile development.

The operations team would like to maintain a space in the cluster where they can enforce strict procedures on who can or cannot manipulate the set of Pods, Services, and Deployments that run the production site.

One pattern this organization could follow is to partition the Kubernetes cluster into two namespaces: development and production.

Let’s create two new namespaces to hold our work.

Use the file [namespace-dev.json](https://kubernetes.io/examples/admin/namespace-dev.json) which describes a development namespace.

Create the development namespace using kubectl.

```
kubectl create -f https://k8s.io/examples/admin/namespace-dev.json
```

Save the following contents into file [namespace-prod.json](https://kubernetes.io/examples/admin/namespace-prod.json) which describes a production namespace:

And then let’s create the production namespace using kubectl.

```shell
kubectl create -f https://k8s.io/examples/admin/namespace-prod.json
```

To be sure things are right, let’s list all of the namespaces in our cluster.

```shell
kubectl get namespaces --show-labels
```

You should get an output similar as follow:

```shell
NAME           STATUS   AGE    LABELS
default        Active   68m    <none>
development    Active   6m8s   name=development
kube-public    Active   68m    <none>
kube-system    Active   68m    <none>
monitoring     Active   50m    <none>
ntnx-logging   Active   57m    monitor=monitoring
production     Active   9s     name=production
```

**Lab finished**