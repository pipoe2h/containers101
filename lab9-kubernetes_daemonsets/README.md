# Lab9 - Kubernetes DaemonSets
The objective of this lab is to get a basic knowledge about how to use Kubernetes DaemonSets.

For this lab you need to access to your virtual machine to run the *kubectl* commands.

## DaemonSet
For this exercise we are going to deploy Nutanix Epoch. Nutanix Epoch runs as a DaemonSet when used with Kubernetes clusters. This means all the workers in a Kubernetes cluster will run an Epoch **collector** pod.

Open [My Nutanix](https://my.nutanix.com) and use your Nutanix credentials to access your own Xi Epoch. If you don't have Epoch, you can use **demo.nutanix.com**

Now that you have your cluster monitored with Nutanix Epoch, let's test that our DaemonSet is working. Go back to your Kubernetes cluster in Karbon and scale-out your cluster with one extra worker node.

**Lab finished**
