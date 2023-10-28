## Integrating HELM Into Microk8s

Don't know what Helm is? Click [Here](https://helm.sh/docs/topics/architecture/#the-purpose-of-helm)!

***
## Table of Contents
**1. Installing Helm**<br>
**2. Deploying a Mern Stack as a Helm Chart**<br>

***
## Installing Helm
This guide shows how to install the Helm CLI. Helm can be installed either from source, or from pre-built binary releases.

### Installing From Binary Release
Every release of Helm provides binary releases for a variety of OSes. These binary versions can be manually downloaded and installed.

<br>

First, Download your desired Binary Release by Clicking [Here](https://github.com/helm/helm/releases)

After the package is downloaded, Unpack it 
```bash
tar -zxvf helm-<version>-<arch>.tar.gz
```

<br>

Find the helm binary in the unpacked directory, and move it to its desired destination 
```bash
sudo mv linux-amd64/helm /usr/local/bin/helm
```

From there, you should be able to run the client and add the stable repo
```bash
helm help
```

***

## Installing From Script
Helm now has an installer script that will automatically grab the latest version of Helm and install it locally.

<br>

You can fetch that script, and then execute it locally. It's well documented so that you can read through it and understand what it is doing before you run it.cript that will automatically grab the latest version of Helm and install it locally.
```bash
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
Yes, you can `curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash` if your feeling spicy.

<br>

If you would like to install via a native package manager Click [Here](https://helm.sh/docs/intro/install/#through-package-managers) for a guide

***
## Deploying a Mern Stack as a Helm Chart
Not sure what MERN Stack is? No worries, Click [Here](https://www.simplilearn.com/tutorials/mongodb-tutorial/what-is-mern-stack-introduction-and-examples)


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
