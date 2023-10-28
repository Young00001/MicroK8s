## Integrating HELM Into Microk8s

Don't know what Helm is? Click [Here](https://helm.sh/docs/topics/architecture/#the-purpose-of-helm)!

***
## Table of Contents
**1. Installing Helm**<br>
**2.**<br>

***
## Installing Helm
This guide shows how to install the Helm CLI. Helm can be installed either from source, or from pre-built binary releases.

### Binary Release
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
mv linux-amd64/helm /usr/local/bin/helm
```

From there, you should be able to run the client and add the stable repo
```bash
helm help
```

***
