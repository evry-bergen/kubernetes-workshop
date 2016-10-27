# Lab 4: Creating and Managing Services

[`Services`][services] provide stable endpoints for [`Pods`][pods] based on a
set of [`Labels`][labels].

In this lab you will create the `monolith` `Service` and "expose" the
`secure-monolith` Pod externally. You will learn how to:

* Create a [`Service`][services]
* Use label selectors to expose a limited set of [`Pods`][pods] externally

[services]: http://kubernetes.io/docs/user-guide/services/
[pods]: http://kubernetes.io/docs/user-guide/pods/
[labels]: http://kubernetes.io/docs/user-guide/labels/

## Tutorial: Create a Service

Explore the monolith service configuration in
[monolith-service.yaml](./monolith-service.yaml):

```
cat monolith-service.yaml
```

Create the monolith service using kubectl:

```
kubectl create -f monolith-service.yaml
```

## Exercise: Interact with the Monolith Service Remotely

### Hints

```
minikube ip
```

```
curl -k https://<MINIKUBE_IP>:31000
```

### Quiz

* Why are you unable to get a response from the `monolith` service?

## Exercise: Explore the monolith Service

### Hints

```
kubectl get services monolith
```

```
kubectl describe services monolith
```

### Quiz

* How many endpoints does the `monolith` service have?
* What labels must a Pod have to be picked up by the `monolith` service?

## Tutorial: Add Labels to Pods

Currently the `monolith` service does not have any endpoints. One way to
troubleshoot an issue like this is to use the `kubectl get pods` command with a
label query.

```
kubectl get pods -l "app=monolith"
```

```
kubectl get pods -l "app=monolith,secure=enabled"
```

> Notice this label query does not print any results

Use the `kubectl label` command to add the missing `secure=enabled` label to the
`secure-monolith` Pod.

```
kubectl label pods secure-monolith 'secure=enabled'
```

View the list of endpoints on the `monolith` service:

```
kubectl describe services monolith
```

### Quiz

* How many endpoints does the `monolith` service have?

## Exercise: Interact with the Monolith Service Remotely

### Hints

```
minikube ip
```

```
curl -k https://<MINIKUBE_IP>:31000
```

## Tutorial: Remove Labels from Pods

In this exercise you will observe what happens when a required label is removed
from a Pod.

Use the `kubectl label` command to remove the `secure` label from the
`secure-monolith` Pod.

```
kubectl label pods secure-monolith secure-
```

View the list of endpoints on the `monolith` service:

```
kubectl describe services monolith
```

### Quiz

* How many endpoints does the `monolith` service have?

## Summary

In this lab you learned how to expose Pods using services and labels.

## Clean Up

When you are done you can exit your open shells and run the following command:

```
kubectl delete -f monolith-service.yaml
```

-----

<p align="right"><a href="../5-deployments">Lab 5: Creating and Managing Deployments ➡️</a></p>
