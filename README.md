# Kubernetes Workshop

In this workshop you will learn how to:

* Set up a [Kubernetes][k8s] cluster locally using [Minikube][minik8s]
* Deploying applications and services using [`kubectl`][kubectl]
* Managing applications using the [Web UI (dashboard)][k8sui]

Kubernetes version: 1.4.0


## 1. Workshop setup

### 1.1 Set up Minikube

1. Download and install [VirtualBox][virtualboxdl].
2. Download and install [`kubectl`][kubectldl].
3. Download and install [Minikube][minik8sdl].
4. Start minikube:

```
$ minikube start
```

### 1.2 Verify your setup

```
$ minikube version
$ minikube status
$ kubectl version
```

### 1.3 Clone this repo

Find a suited directory on your machine to clone this repository.

```
$ git clone https://github.com/evry-bergen/kubernetes-workshop.git
```

## 2. Labs

1. [Creating and managing pods](./labs/1-pods)

## 3. Reference

* [Kubernetes][k8s]
* [Docker][docker]

[docker]: https://docs.docker.com/
[k8s]: http://kubernetes.io/docs/
[k8sui]: http://kubernetes.io/docs/user-guide/ui/
[kubectl]: http://kubernetes.io/docs/user-guide/kubectl-overview/
[kubectldl]: http://kubernetes.io/docs/getting-started-guides/minikube/#install-kubectl
[minik8s]: https://github.com/kubernetes/minikube
[minik8sdl]: https://github.com/kubernetes/minikube/releases/latest
[virtualboxdl]: https://www.virtualbox.org/wiki/Downloads
