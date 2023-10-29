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
MongoDB uses port 27017 by default, to ensure that the port is free you can use the following command:
```bash
netstat -tuln | grep 27017
```

<br>

To start a MongoDB Service Deployment, we will first create a working deployment directory and add a `.yaml` file:
```bash
mkdir -p ~/Deployment/MongoDB && cd ~/Deployment/MongoDB && gedit mongodb-svc.yaml
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

<br>

Afterwards, we can now deploy our manifest file:
```bash
sudo microk8s kubectl apply -f mongodb-svc.yaml
```

<br>

Check to see if the service is running:
```bash
sudo microk8s kubectl get svc
```

***
## MongoDB Pod Deployment
To deploy our StatefulSet MongoDB Pods we will start my ensuring we are in our `~/Deployment/MongoDB` directory and we will also create our manifest file labeled `mongodb-statefulset.yaml`
```bash
cd ~/Deployment/MongoDB && gedit mongodb-statefulset.yaml
```

### Contents of `mongodb-statefulset.yaml` file
```yaml
apiVersion: v1
kind: StatefulSet
metadata:
  name: mongodb
spec:
  serviceName: mongodb
  replicas: 1
  selector:
    matchLabels:
      app: mongodb
  template:
    metadata:
      labels:
        app: mongodb
        selector: mongodb
    spec:
      containers:
        - name: mongodb
          image:
          ports:
            - containerPort: 27017
          volumeMounts:
            - name: pvc
              mountPath: data/db
  volumeClaimTeplates:
    - metadata:
        name: pvc
      spec:
        accessModes:
          - ReadWriteOnce
        resources:
          requests:
            storage: 1Gi

```
