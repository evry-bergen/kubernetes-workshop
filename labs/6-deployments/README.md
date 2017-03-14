# Lab 6: Creating and Managing Deployments

[`Deployments`][deployments] abstract away the low level details of managing
[`Pods`][pods]. `Pods` are tied to the lifetime of the node they are created on.
When a [`Node`][nodes] goes away so does its `Pods`. [ReplicaSets][replicasets]
can be used to ensure one or more replicas of a `Pod` are always running, even
when `Nodes` fail.

`Deployments` sit on top of `ReplicaSets` and add the ability to define how
updates to `Pods` should be rolled out.

In this lab we will combine everything we learned about `Pods` and
[`Services`][services] to breakup the monolith application into smaller
Services. You will create 3 `Deployments`, one for each `Service`:

* frontend
* auth
* hello

You will also define internal services for the `auth` and `hello` deployments
and an external service for the `frontend` deployment.

[deployments]: http://kubernetes.io/docs/user-guide/deployments/
[nodes]: http://kubernetes.io/docs/admin/node/
[pods]: http://kubernetes.io/docs/user-guide/pods/
[replicasets]: http://kubernetes.io/docs/user-guide/replicasets/
[services]: http://kubernetes.io/docs/user-guide/services/

## Tutorial: Creating Deployments

### Create and Expose the Auth Deployment

```
kubectl create -f auth/deployment.yaml
```

```
kubectl describe deployments auth
```

```
kubectl create -f auth/service.yaml
```

### Create and Expose the Hello Deployment

```
kubectl create -f hello/deployment.yaml
```

```
kubectl describe deployments hello
```

```
kubectl create -f hello/service.yaml
```

### Create and Expose the Frontend Deployment


```
kubectl create configmap nginx-frontend-conf --from-file=frontend/frontend.conf
```

```
kubectl create -f frontend/deployment.yaml
```

```
kubectl create -f frontend/service.yaml
```

## Tutorial: Scaling Deployments

Behind the scenes `Deployments` manage `ReplicaSets`. Each `Deployment` is mapped to
one active `ReplicaSet`. Use the `kubectl get replicasets` command to view the
current set of replicas.

```
kubectl get replicasets
```

`ReplicaSets` are scaled through the `Deployment` for each service and can be
scaled independently. Use the `kubectl scale` command to scale the `hello`
deployment:

```
kubectl scale deployments hello --replicas=3
```

```
kubectl describe deployments hello
```

```
kubectl get pods
```

```
kubectl get replicasets
```

## Exercise: Scaling Deployments

In this exercise you will scale the `frontend` deployment using an existing
deployment configuration file.

### Hints

```
vim frontend/deployment.yaml
```

```
kubectl apply -f frontend/deployment.yaml
```

## Exercise: Interact with the Frontend Service

### Hints

<!--
```
minikube service frontend --https --url
```
-->


```
minikube ip
```

```
curl -k https://<MINIKUBE-IP>:31000
```

## Summary

Deployments are the preferred way to manage application deployments. You learned
how to create, expose and scale deployments.

-----

<p align="right"><a href="../7-updates">Lab 7: Rolling out Updates ➡️</a></p>
