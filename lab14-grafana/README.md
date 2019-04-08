# Lab14 - Grafana
The objective of this lab is to deploy Grafana and integrate with the existing Prometheus available in any Kubernetes cluster deployed with Karbon.

For this lab you need to access to your virtual machine to run the *kubectl* commands.

## Grafana
Grafana provides visualisation of your monitoring metrics. The datasource in this case will be Prometheus which is available in any Kubernetes cluster deployed with Karbon.

Use as a reference the following material:

* [Grafana manifests](https://github.com/coreos/prometheus-operator/tree/master/contrib/kube-prometheus/manifests)

**Tip:** Make sure you only use the grafana manifests available in the link above. Also, you will need to make grafana available externally for its consumption. Remember that Prometheus is running in the **monitoring** namespace and Grafana should run in the same.

**Lab finished**