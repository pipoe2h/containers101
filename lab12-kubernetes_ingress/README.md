# Lab12 - Kubernetes Ingress Controller
The objective of this lab is to get a basic knowledge about how to use Kubernetes Ingress. For this exercise we are going to expose the simple webapp from *Lab11*.

For this lab you need to access to your virtual machine to run the *kubectl* commands.

## Ingress Controller
Follow the instructions available in NGINX Ingress Controller website to deploy the ingress controller:

* [Installation Guide](https://kubernetes.github.io/ingress-nginx/deploy/)

### TL;DR
Deploy Nginx Ingress Controller

```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
```

Deploy Nginx Ingress Controller Service

```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/provider/baremetal/service-nodeport.yaml
```

To check if the ingress controller pods have started, run the following command:

```shell
kubectl get pods --all-namespaces -l app.kubernetes.io/name=ingress-nginx --watch
```

## Name based virtual hosting
Now that you have the Ingress Controller pod running, you need to create an Ingress manifest for the simple webapp from Lab11. Have a look to [name based virtual hosting](https://kubernetes.io/docs/concepts/services-networking/ingress/#name-based-virtual-hosting)

**Tip:** 
* *host*: app.<any_worker_IP>.nip.io
* *serviceName*: You will need to find it from previous exercise using **kubectl**
* *servicePort*: You will need to find it from previous exercise using **kubectl**

Once you have created the manifest file, apply the manifest and test from a web browser you are able to visit the website using your URL. Ie.: app.10.10.56.194.nip.io:<port>

**Lab finished**