## Mern Stack Deployment in Microk8s
- What is [Mern]()?
- What is a [Stack]()?

***
## Table of Contents
**1. Prerequisites**<br>
**2. Microk8s Addons**<br>
**3. Service Deplyoment**<br>
**4. Pod Deployment**<br>

***
## Prerequisites
Ensure that you have an active **Microk8s Cluster**<br>
_If you need a guide on how to set-up a Microk8s Cluster you can follow my guide [Here](../../README.md)_

***
## Microk8s Addons
The following Addons are recommended for this stack deployment:
```bash
sudo microk8s enable dns dashboard storage ingress
```

`dns`: Enables CoreDNS for DNS resolution.<br>

`dashboard`: Enables the Kubernetes dashboard for web-based management.<br>

`storage`: Enables storage provisioners.<br>

`ingress`: Enables Ingress controller for routing external traffic to services.
