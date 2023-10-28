## Integrating HELM Into Microk8s

Don't know what Helm is? Click [Here](https://helm.sh/docs/topics/architecture/#the-purpose-of-helm)!

***
## Table of Contents
**1. Enabling Helm**<br>
**2. Deploying a Mern Stack as a Helm Chart**<br>

***
## Enableling Helm on your Microk8s Cluster
In order to enable the Helm Service you can type the following command:
```bash
sudo microk8s enable helm
```


***
## Deploying a Mern Stack as a Helm Chart
Not sure what MERN Stack is? No worries, Click [Here](https://www.simplilearn.com/tutorials/mongodb-tutorial/what-is-mern-stack-introduction-and-examples)

<br>


<br>



### Explanation
```bash
microk8s kubectl create serviceaccount --namespace kube-system tiller
```
`microk8s kubectl`: This command is used to run kubectl commands in the context of MicroK8s.<br>

`create serviceaccount`: This part of the command instructs kubectl to create a new service account.<br>

`--namespace kube-system`: Specifies the namespace in which the service account will be created. In this case, it's the kube-system namespace, which is a common namespace for system components in Kubernetes.<br>

`tiller`: This is the name of the service account being created. Tiller is the server-side component of Helm, and it's used to manage and deploy Helm charts.

<br>

```bash
microk8s kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller:
```
`create clusterrolebinding`: This command is used to create a cluster role binding. A cluster role binding associates a cluster role (in this case, cluster-admin) with a service account.<br>

`tiller-cluster-rule`: This is the name of the cluster role binding.<br>

`--clusterrole=cluster-admin`: Specifies the cluster role to be bound to the service account. In this case, the cluster-admin cluster role grants full administrative access to the cluster.<br>

`--serviceaccount=kube-system:tiller`: Specifies the service account that the cluster role binding is associated with. This binds the tiller service account in the kube-system namespace to the cluster-admin role, effectively granting Tiller administrative access to the cluster.

<br>

```bash
microk8s helm init --service-account tiller
```
`microk8s helm init`: Initializes Helm within the MicroK8s cluster.<br>

`--service-account tiller`: Specifies the service account to be used by Tiller. In this case, it sets Tiller to use the tiller service account you created earlier.
