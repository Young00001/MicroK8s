### How to Integrate MongoDB into your Microk8s Cluster Using a StatefulSet

- What is [MongoDB]()?<br>
- What is [StatefulSet]()?
***
## Table of Contents
**1. MongoDB Service Deployment**<br>
**2. MongoDB Pod Deployment**<br>
**3. Accessing MongoDB Pods**<br>

***
## MongoDB Service Deployment
To start a MongoDB Service Deployment, we will first create a working deployment directory and add a `.yaml` file:
```bash
mkdir -p ~/Deployment/MongoDB && cd ~/Deployment/MongoDB
gedit mongodb-svc.yaml
```

### Contents of `mongodb-svc.yaml` file
```yaml
apiVersion: v1
kind: Service
metadata:
  name: mongodb
  labels:
    app: mongodb
spec:
  clusterIP: None
  selector:
    app: mongodb
  ports:
    - port: 27017
      targetPort: 27017
```
Click [Here](https://www.yamllint.com/) for a **.yaml validator** to ensure you have the correct formatting.
