# kube-gateway
This project is about the use and configuration of the k8s gateway API.

## Reference
1. https://docs.nginx.com/nginx-gateway-fabric
2. https://docs.nginx.com/nginx-gateway-fabric/install 

## Add certificates for secure authentication
1. Install Gateway API CRDs
```console
kubectl kustomize "https://github.com/nginx/nginx-gateway-fabric/config/crd/gateway-api/standard?ref=v2.3.0" | kubectl apply -f -
```
2. Create the CA issuer
```console
kubectl create namespace nginx-gateway
```
```console
kubectl apply -f ca-issuer.yaml -n nginx-gateway
```
3. Create server and client certificates
```console
kubectl apply -f server-tls.yaml -n nginx-gateway
```
```console
kubectl apply -f agent-tls.yaml -n nginx-gateway
```
4. Confirm the Secrets have been created  
You should see the Secrets created in the nginx-gateway namespace:
```console
kubectl -n nginx-gateway get secrets
```

## Install NGINX Gateway Fabric with Helm
### Deploy NGINX Gateway Fabric
1. Install the ctrl plane from the OCI registry
```console
helm install ngf oci://ghcr.io/nginx/charts/nginx-gateway-fabric --create-namespace -n nginx-gateway --set nginx.service.type=NodePort
```

### Uninstall NGINX Gateway Fabric
```console
helm uninstall ngf -n nginx-gateway
```

## Deploy a Gateway for data plane instances  
Create an example in the dataplane-example directory to demonstrate how to deploy a dataplane instance

### Test
```console
export GW_PORT=31954
curl --resolve nginx-hello.example.com:$GW_PORT:$GW_IP http://nginx-hello.example.com:$GW_PORT/
```
