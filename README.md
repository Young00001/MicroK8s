# MicroK8s: The Kubernetes Solution for Linux

## Table of Contents:
**1. Installation**<br>
**2. Status Check**<br>
**3. Turn on Services**<br>
**4. Start using Kubernetes**<br>
**5. Access Kubernetes Dashboard**
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
