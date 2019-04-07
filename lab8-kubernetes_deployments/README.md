# Lab8 - Kubernetes Deployments
The objective of this lab is to get a basic knowledge about how to use Kubernetes Deployemnts.

For this lab you need to access to your virtual machine to run the *kubectl* commands.

## Create pods in each namespace
A Kubernetes namespace provides the scope for Pods, Services, and Deployments in the cluster.

Users interacting with one namespace do not see the content in another namespace.

To demonstrate this, let’s spin up a simple Deployment and Pods in the development namespace.

We first check what is the current context:

```shell
kubectl config view
```

```shell
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://10.10.56.199:443
  name: XYZ-Karbon
contexts:
- context:
    cluster: XYZ-Karbon
    user: default-user
  name: XYZ-Karbon-context
current-context: default-user
kind: Config
preferences: {}
users:
- name: default-user
  user:
    token: eyJhbGciOiJSUzI1NiJ9.eyJ1c2VyX3Byb2ZpbGUiOiJ7XCJ1c2VybmFtZVwiOlwiYWRtaW5cIixcInVpZFwiOlwiMDAwMDAwMDAtMDAwMC0wMDAwLTAwMDAtMDAwMDAwMDAwMDAwXCIsXCJncm91cHNcIjpbXCJzeXN0ZW06bWFzdGVyc1wiXX0iLCJpc3MiOiJBdGhlbmEiLCJpYXQiOjE1NTQ2Mjk2MjIsImV4cCI6MTU1NDcxNjAyMn0.JWeArFaNsj97pFuPT-KC1pXaOT9sRWRdpSRDSVHzx5vgphVwa0n7zeolFYGqs4f2oXxfuFteLXPkfFZdEHcpIAG5GUOZKdaZH3nxdONbHmV9sH1U-iYz4Xcx0RONvavztTSbUYHpUUzOIG8iCP1bQCVkLzQTlOpjNEHK2QHSscTypco6mtKCjPxxeUdNEvu8QifEUXjhCtxIFm6XIUgvn4X0TQ_YLHlm0phQ9-3P2rg3Q5RHZ6orKPam7mdiMEtsgYGECCEbCIrj5Cu5gNHO-nRbs9OS-96plZASzE91GLFaLPTPpjV4GwBNYFn4IwDdAEUGOBygLJVDwfA2-yzkpA
```

```shell
kubectl config current-context
```

```shell
XYZ-Karbon-context
```

The next step is to define a context for the kubectl client to work in each namespace. The value of “cluster” and “user” fields are copied from the current context.

```shell
kubectl config set-context dev --namespace=development \
  --cluster=XYZ-Karbon \
  --user=default-user
```

```shell
kubectl config set-context prod --namespace=production \
  --cluster=XYZ-Karbon \
  --user=default-user
```

By default, the above commands adds two contexts that are saved into file **.kube/config**. You can now view the contexts and alternate against the two new request contexts depending on which namespace you wish to work against.

To view the new contexts:

```shell
kubectl config view
```

```
apiVersion: v1
clusters:
- cluster:
    certificate-authority-data: DATA+OMITTED
    server: https://10.10.56.199:443
  name: XYZ-Karbon
contexts:
- context:
    cluster: XYZ-Karbon
    user: default-user
  name: XYZ-Karbon-context
- context:
    cluster: XYZ-Karbon
    namespace: development
    user: default-user
  name: dev
- context:
    cluster: XYZ-Karbon
    namespace: production
    user: default-user
  name: prod
current-context: XYZ-Karbon-context
kind: Config
preferences: {}
users:
- name: default-user
  user:
    token: eyJhbGciOiJSUzI1NiJ9.eyJ1c2VyX3Byb2ZpbGUiOiJ7XCJ1c2VybmFtZVwiOlwiYWRtaW5cIixcInVpZFwiOlwiMDAwMDAwMDAtMDAwMC0wMDAwLTAwMDAtMDAwMDAwMDAwMDAwXCIsXCJncm91cHNcIjpbXCJzeXN0ZW06bWFzdGVyc1wiXX0iLCJpc3MiOiJBdGhlbmEiLCJpYXQiOjE1NTQ2Mjk2MjIsImV4cCI6MTU1NDcxNjAyMn0.JWeArFaNsj97pFuPT-KC1pXaOT9sRWRdpSRDSVHzx5vgphVwa0n7zeolFYGqs4f2oXxfuFteLXPkfFZdEHcpIAG5GUOZKdaZH3nxdONbHmV9sH1U-iYz4Xcx0RONvavztTSbUYHpUUzOIG8iCP1bQCVkLzQTlOpjNEHK2QHSscTypco6mtKCjPxxeUdNEvu8QifEUXjhCtxIFm6XIUgvn4X0TQ_YLHlm0phQ9-3P2rg3Q5RHZ6orKPam7mdiMEtsgYGECCEbCIrj5Cu5gNHO-nRbs9OS-96plZASzE91GLFaLPTPpjV4GwBNYFn4IwDdAEUGOBygLJVDwfA2-yzkpA
```

Let’s switch to operate in the **development** namespace.

```shell
kubectl config use-context dev
```

You can verify your current context by doing the following:

```shell
kubectl config current-context
```

```shell
dev
```

At this point, all requests we make to the Kubernetes cluster from the command line are scoped to the **development** namespace.

Let’s create some contents.

```shell
kubectl run snowflake --image=kubernetes/serve_hostname --replicas=2
```

We have just created a deployment whose replica size is 2 that is running the pod called **snowflake** with a basic container that just serves the hostname. Note that **kubectl run** creates deployments only on Kubernetes cluster >= v1.2. If you are running older versions, it creates replication controllers instead. If you want to obtain the old behavior, use **--generator=run/v1** to create replication controllers. See [kubectl run](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands/#run) for more details.

```shell
kubectl get deployment
```

```shell
NAME        DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
snowflake   2         2         2            2           2m
```

```shell
kubectl get pods -l run=snowflake
```

```shell
NAME                         READY     STATUS    RESTARTS   AGE
snowflake-3968820950-9dgr8   1/1       Running   0          2m
snowflake-3968820950-vgc4n   1/1       Running   0          2m
```

And this is great, developers are able to do what they want, and they do not have to worry about affecting content in the **production** namespace.

Let’s switch to the **production** namespace and show how resources in one namespace are hidden from the other.

```shell
kubectl config use-context prod
```

The **production** namespace should be empty, and the following commands should return nothing.

```shell
kubectl get deployment
kubectl get pods
```

Production likes to run cattle, so let’s create some cattle pods.

```shell
kubectl run cattle --image=kubernetes/serve_hostname --replicas=5

kubectl get deployment
```

```shell
NAME      DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
cattle    5         5         5            5           10s
```

```shell
kubectl get pods -l run=cattle
```

```shell
NAME                      READY     STATUS    RESTARTS   AGE
cattle-2263376956-41xy6   1/1       Running   0          34s
cattle-2263376956-kw466   1/1       Running   0          34s
cattle-2263376956-n4v97   1/1       Running   0          34s
cattle-2263376956-p5p3i   1/1       Running   0          34s
cattle-2263376956-sxpth   1/1       Running   0          34s
```

At this point, it should be clear that the resources users create in one namespace are hidden from the other namespace.

## (Optional) [Run a Stateless Application Using a Deployment](https://kubernetes.io/docs/tasks/run-application/run-stateless-application-deployment/)

**Lab finished**
