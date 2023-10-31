## Mern Stack Deployment in Microk8s
- What is [Mern]()?
- What is a [Stack]()?

***
## Table of Contents
**1. Prerequisites**<br>
**2. Microk8s Addons**<br>
**3. Service Deplyoment**<br>
**4. Pod Deployment**<br>
**5. Connecting to Mongodb Instance**<br>

***
## Prerequisites
Ensure that you have an active **Microk8s Cluster**<br>
_If you need a guide on how to set-up a Microk8s Cluster you can follow my guide [Here](../../README.md)_

***
## Microk8s Addons
The following Addons are recommended for this stack deployment<br>
Enable the following addons from the Control-Plane Node:
```bash
sudo microk8s enable dns dashboard storage ingress
```

`dns`: Enables CoreDNS for DNS resolution.<br>

`dashboard`: Enables the Kubernetes dashboard for web-based management.<br>

`storage`: Enables storage provisioners.<br>

`ingress`: Enables Ingress controller for routing external traffic to services.

***
## Service & Pod Deployment
For Deploying all services and pods within the stack you can use the following manifest files by clicking [Here]()
```bash
sudo microk8s kubectl apply -f .
```

***
## Connecting to MongoDB Instance
In order to connect to your Mongodb Instance you can first obtain the IP address:
```bash
sudo microk8s kubectl describe pod pod_name
```

<br>

After obtaining the pods IP address we can download the **mongodb-mongosh** by clicking [Here](https://downloads.mongodb.com/compass/mongodb-mongosh_1.10.6_amd64.deb)<br>
Once Downloaded you can depackage the `.deb` file:
```bash
sudo dpkg -i file.deb
```

<br>

Finally, we can connect to our Mongodb Instance by typing the following command:
```bash
mongo IP_Address:27017
```
