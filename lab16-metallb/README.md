# Lab16 - MetalLB
The objective of this lab is to use MetalLB to expose a Kubernetes Service using LoadBalancer type.

For this lab you need to access to your virtual machine to run the *kubectl* commands.

## MetalLB
MetalLB is .

Use as a reference the following material:

* [MetalLB Installation](https://metallb.universe.tf/installation/)

* [MetalLB Configuration](https://metallb.universe.tf/configuration/#layer-2-configuration). Ask the instructor for what static IP address you can use.

Now that you have MetalLB running, you don't need to expose your services using NodePort. Let's expose the Grafana dashboard with LoadBalancer.

**Lab finished**