# Lab 1: Creating and Managing Pods

At the core of Kubernetes is the [`Pod`][pod]. Pods represent a logical
application and hold a collection of one or more containers and volumes. In this
lab you will learn how to:

* Write a Pod configuration file
* Create and inspect Pods
* Interact with Pods remotely using kubectl

In this lab you will create a Pod named `monolith` and interact with it using
the kubectl command line tool.

## Tutorial: Creating Pods

Explore the `monolith` Pod configuration file ([monolith.yaml](./monolith.yaml)):

```
cat monolith.yaml
```

Use the [`kubectl create`][kubectl_create] command to create the `monolith` Pod
using kubectl:

```
kubectl create -f monolith.yaml
```

## Exercise: View Pod details

Use the [`kubectl get`][kubectl_get] and [`kubect describe`][kubectl_describe]
commands to view details for the `monolith` Pod:

### Hints

```
kubectl get pods
```

```
kubectl describe pods <pod-name>
```

### Quiz

* What is the IP address of the `monolith` Pod?
* What node is the `monolith` Pod running on?
* What containers are running in the `monolith` Pod?
* What are the labels attached to the `monolith` Pod?
* What arguments are set on the `monolith` container?

## Exercise: Interact with a Pod remotely

Pods are allocated a private IP address by default and cannot be reached outside
of the cluster. Use the [`kubectl port-forward`][kubectl_port-forward] command
to map a local port to a port inside the `monolith` Pod.

### Hints

Use two terminals. One to run the `kubectl port-forward` command, and the other
to issue `curl` commands.

```
kubectl port-forward monolith 10080:80
```

Open a new terminal window for the following commands:

```
curl http://127.0.0.1:10080
```

```
curl http://127.0.0.1:10080/secure
```

```
curl -u user http://127.0.0.1:10080/login
```

> Type `password` at the prompt.

```
curl -H "Authorization: Bearer <token>" http://127.0.0.1:10080/secure
```

> Use the JWT token from the previous login.

## Exercise: View the logs of a Pod

Use the [`kubectl logs`][kubectl_logs] command to view the logs for the
`monolith` Pod:

```
kubectl logs monolith
```

> Use the `-f` flag and observe what happens.

## Exercise: Run an interactive shell inside a Pod

Use the [`kubectl exec`][kubectl_exec] command to run an interactive shell
inside the `monolith` Pod:

```
kubectl exec monolith --stdin --tty -c monolith /bin/sh
```

## Clean Up

When you are done you can exit your open shells and run the following command:

```
kubectl delete -f monolith.yaml
```

[pod]: http://kubernetes.io/docs/user-guide/pods/
[kubectl_create]: http://kubernetes.io/docs/user-guide/kubectl/kubectl_create/
[kubectl_describe]: http://kubernetes.io/docs/user-guide/kubectl/kubectl_describe/
[kubectl_exec]: http://kubernetes.io/docs/user-guide/kubectl/kubectl_exec/
[kubectl_get]: http://kubernetes.io/docs/user-guide/kubectl/kubectl_get/
[kubectl_logs]: http://kubernetes.io/docs/user-guide/kubectl/kubectl_logs/
[kubectl_port-forward]: http://kubernetes.io/docs/user-guide/kubectl/kubectl_port-forward/

-----

<p align="right"><a href="../2-health">Lab 2: Monitoring and Health Checks ➡️</a></p>
