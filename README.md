# MicroK8s: The Kubernetes Solution for Linux

## Table of Contents:
**[1. Installation](https://github.com/Young00001/MicroK8s/blob/main/README.md#1-installation)**<br>
**[2. Status Check](https://github.com/Young00001/MicroK8s/blob/main/README.md#2-check-the-status-while-kubernetes-initializes)**<br>
**[3. Turn on Services](https://github.com/Young00001/MicroK8s/blob/main/README.md#3-turn-on-the-services-you-want)**<br>
**[4. Start using Kubernetes](https://github.com/Young00001/MicroK8s/tree/main#4-start-using-kubernetes)**<br>
**[5. Access Kubernetes Dashboard](https://github.com/Young00001/MicroK8s/tree/main#5-access-the-kubernetes-dashboard)**
**[6. Add a Worker Node]()**
***
## 1. Installation
Install MicroK8s on Linux
```bash
sudo snap install microk8s --classic
```
Don't have the `snap` command? [Get snap Here](https://snapcraft.io/docs/installing-snapd)

***
## 2. Check the Status while Kubernetes Initializes
```bash
microk8s status --wait-ready
```

***
## 3. Turn on the Services you want
```bash
microk8s enable dashboard
microk8s enable dns
microk8s enable registry
microk8s enable istio
```
_Try `microk8s enable --help` for a list of available services and optional features. `microk8s disable <name>` turns off a service._

***
## 4. Start using Kubernetes
```bash
microk8s kubectl get all --all-namespaces
```

***
## 5. Access the Kubernetes Dashboard
```bash
microk8s dashboard-proxy
```
***
## 6. Add a Worker Node
