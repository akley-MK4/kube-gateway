# kube-gateway
This project is about the use and configuration of the k8s gateway API.

## Reference
https://gateway-api.sigs.k8s.io/  

## Install

1. Install gateway CRDs from the standard channel  
```console
kubectl apply --server-side -f https://github.com/kubernetes-sigs/gateway-api/releases/download/v1.4.1/standard-install.yaml
```
2. Install a gateway controller  
From page [Gateway Controller Implementation](https://gateway-api.sigs.k8s.io/implementations/) choose a supported controller, such as NGINX Gateway Fabric.