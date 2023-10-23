# MicroK8s: The Kubernetes Solution for Linux

## Table of Contents:
**[1. Installation](https://github.com/Young00001/MicroK8s/blob/main/README.md#1-installation)**<br>
**[2. Status Check](https://github.com/Young00001/MicroK8s/blob/main/README.md#2-check-the-status-while-kubernetes-initializes)**<br>
**[3. Turn on Services](https://github.com/Young00001/MicroK8s/blob/main/README.md#3-turn-on-the-services-you-want)**<br>
**[4. Start using Kubernetes](https://github.com/Young00001/MicroK8s/blob/main/README.md#4-start-using-kubernetes)**<br>
**[5. Access Kubernetes Dashboard](https://github.com/Young00001/MicroK8s/blob/main/README.md#5-access-the-kubernetes-dashboard)**<br>
**[6. Add a Worker Node](https://github.com/Young00001/MicroK8s/blob/main/README.md#6-add-a-worker-node)**<br>
**[7. Pod Deployment](https://github.com/Young00001/MicroK8s/blob/main/README.md#7-pod-deployment)**
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
sudo microk8s status --wait-ready
```

***
## 3. Turn on the Services you want
```bash
sudo microk8s enable dashboard
sudo microk8s enable dns
sudo microk8s enable registry
sudo microk8s enable istio
```
Try `microk8s enable --help` for a list of available services and optional features.<br> 

`microk8s disable <name>` turns off a service.

***
## 4. Start using Kubernetes
```bash
sudo microk8s kubectl get all --all-namespaces
```

***
## 5. Access the Kubernetes Dashboard
```bash
sudo microk8s dashboard-proxy
```
***
## 6. Add a Worker Node
Ensure that the hostname of the joining **Worker Node** is correctly associated with its IP address in your network's DNS or hosts file:
```bash
sudo nano /etc/hosts
```
Add your **Worker** and **Control Plane** Nodes to the File:
```bash
IP Address      Hostname            Description
------------------------------------------------------
127.0.0.1       localhost           Loopback Address
192.168.x.x     microk8s-master     Control Plane Node
192.168.x.x     microk8s-worker     Worker Node
```

<br>

Now, we can start the process of joining our worker node to the microk8s cluster:
```bash
sudo microk8s add-node
```

This will return some joining instructions which should be executed on the MicroK8s instance that you wish to join to the cluster **(NOT THE NODE YOU RAN add-node FROM)**

```bash
From the node you wish to join to this cluster, run the following:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05

Use the '--worker' flag to join a node as a worker not running the control plane, eg:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05 --worker

If the node you are adding is not reachable through the default interface you can use one of the following:
microk8s join 192.168.1.230:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
microk8s join 10.23.209.1:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
microk8s join 172.17.0.1:25000/92b2db237428470dc4fcfc4ebbd9dc81/2c0cb3284b05
```

<br>

Afterwards, we will run the following command to ensure that our **Worker Node** is now in our cluster:
```bash
sudo microk8s kubectl get nodes
or
sudo microk8s kubectl get no
```

***
## 7. Pod Deployment
This is a simple example of a pod deployment using a docker container

<br>

**_(OPTIONAL)_**  
In order to keep a clean workspace you can do the following:
```bash
mkdir ~/Deployment && cd ~/Deployment
```

<br>

Next, we can create a manifest file using a `.yaml` extension
```bash
nano pod_name.yaml
```
Here is an example manifest file that you can use and modify with your own configurations:
```bash
apiVersion: apps/v1
kind: Deployment
metadata:
  name: pod-name
spec:
  replicas: 1
  selector:
    matchLabels:
      app: pod-name
  template:
    metadata:
      labels:
        app: pod-name
    spec:
      containers:
      - name: pod
        image: image_name:tag
        command: ["tail", "-f", "/dev/null"]
```

<br>

Now that we have our manifest file we can deploy our new pod using our **Master Node**:
```bash
sudo microk8s kubectl apply -f pod_name.yaml
```
To view your pod use the following command:
```bash
sudo microk8s kubectl get pods
```
For a more desciptive view of your pod use:
```bash
sudo microk8s kubectl describe pod pod_name
```
