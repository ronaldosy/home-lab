## Install kubernetes
Run dry run with first

```bash
sudo kubeadm init --config kubeadm-config/kubeadm-config.yaml --dry-run
```
>**Note:**
To generate config file we can use ```kubeadm config print init-defaults```, and edit the content according to your lab environment. Check the kubeadm Configuation (v1beta3) documentation: https://kubernetes.io/docs/reference/config-api/kubeadm-config.v1beta3/
Please check the documenation according the apiVersion that you are using.

After everythong ok run
```bash
sudo kubeadm init --config kubeadm-config/kubeadm-config.yaml --dry-run
```

## Install flannel networking add-on

I suggest to download manifest file first

```
wget https://github.com/flannel-io/flannel/releases/latest/download/kube-flannel.yml
```

After the manifest downloaded, run kubectl apply
```
kubectl apply -f kube-flannel.yml
```
For detail about flannel check documentation: https://github.com/flannel-io/flannel

## Install metallb

Download the manifest file first (this is optional), for latest version check the metallb documentation: https://metallb.io/installation/

```bash
curl https://raw.githubusercontent.com/metallb/metallb/v0.14.9/config/manifests/metallb-native.yaml -o metallb/metallb-native-0.4.19.yaml
```
Install metallb using kubectl

```bash
kubectl apply -f metallb/metallb-native-0.4.19.yaml
```

On this lab I'm using L2 mode. We need to apply the configuration for L2 mode. 
For detail check the metallb documentation for L2 mode 


```bash
kubectl apply -f metallb/metallb-l2-config.yaml
```
>**Note:**
For address pools use the same subnet as the worker node, make sure the IP Adresses range not use by other nodes.


## Install nginx ingress 
Because I use metallb as LoadBalance, I use the quick start guide for nginx-ingress installation. Check the documentation: https://kubernetes.github.io/ingress-nginx/deploy/ 

Check also the compatibility version at https://github.com/kubernetes/ingress-nginx

Download the ingress-nginx manifest file (this is optional you can also use helm to install ingress NGINX controller)

```bash
curl https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.11.3/deploy/static/provider/cloud/deploy.yaml -o ingress-nginx-v1.11.3.yaml
```

Install ingress NGINX controller
```bash
kubectl apply -f ingress-nginx-v1.11.3.yaml
```
