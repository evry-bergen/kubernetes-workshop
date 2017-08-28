# Lab 5: Routing Ingress Traffic

A Kubernetes [`Service`](services) identifies a set of [`pods`](pods) using
[`label`](labels) selectors. Unless otherwise configured, Services are only
reachable from within the cluster network.

In the previous lab assignment we created the `monolith` service available
through the fixed port `31000`. While this may be an acceptable approach for a
single service, it does not scale, and soon you'll end up with conflicting ports.

An [`Ingress`](ingress) is a collection of rules that allow inbound connections
to reach cluster services.

```
                                                         internet
          internet                                           |
              |                                         [ Ingress ]
        ------------                                    --|-----|--
        [ Services ]                                    [ Services ]
```

[services]: http://kubernetes.io/docs/user-guide/services/
[pods]: http://kubernetes.io/docs/user-guide/pods/
[labels]: http://kubernetes.io/docs/user-guide/labels/
[ingress]: https://kubernetes.io/docs/user-guide/ingress/

## Tutorial: Enable the Ingress Controller

In order for the `Ingress` resource to work, the cluster must have an Ingress
controller running. This is unlike other types of controllers, which typically
run as part of the `kube-controller-manager` binary, and which are typically
started automatically as part of cluster creation.

On public clouds such as Google Cloud and AWS native Load Balancers can be used
for routing ingress traffic. On on-premis solutions [Træfik](traefik) is a
popular solution.

Luckily `minikube` provides an Ingress controller for us; all we need to do is
enable it:

```
minikube addons list
```

```
minikube addons enable ingress
```

[traefik]: https://github.com/containous/traefik

## Tutorial: Create an Ingress

Explore the monolith ingress configuration in
[monolith-ingress.yaml](./monolith-ingress.yaml):

```
cat monolith-ingress.yaml   # on mac/linux
type monolith-ingress.yaml  # on window
```

Create the monolith ingress using kubectl:

```
kubectl apply -f monolith-ingress.yaml
```

## Exercise: Explore the Monolith Ingress

### Hints

```
kubectl get ingress monolith
```

```
kubectl describe ingress monolith
```

### Quiz

* What is the public hostname of the Ingress?
* What is the the public IP and port for the Ingress?
* What is the backend service?

## Exercise: Access the Monolith Ingress

### Hints

```
minikube ip
```

```
curl monolith.com --resolve monolith.com:80:<MINIKUBE_IP>
```

## Tutorial: Change the Ingress hostname

```
kubectl patch ingress monolith --type=json \
  -p="[{\"op\": \"replace\", \"path\": \"/spec/rules/0/host\", \"value\": \"awesome.com\"}]"
```

```
curl awesome.com --resolve awesome.com:80:<MINIKUBE_IP>
```

## Summary

In this lab you learned how to route external traffic to services with Ingress.

## Clean Up

When you are done you can exit your open shells and run the following commands:

```
kubectl delete pod secure-monolith
kubectl delete configmap nginx-proxy-conf
kubectl delete service monolith
kubectl delete ingress monolith
```

-----

<p align="right"><a href="../6-deployments">Lab 6: Creating and Managing Deployments ➡️</a></p>
