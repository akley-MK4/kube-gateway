# Envoy-Gateway
This project is about the use and configuration of the k8s gateway API.

## Reference
https://gateway.envoyproxy.io/    

## Install Envoy Gateway with Helm
### Deploy

1. Select a version and export the file 'values.yaml' to the current directory  
```console
helm show values oci://docker.io/envoyproxy/gateway-helm --version v1.8.2 > values.yaml
```

2. Install the ctrl plane from the OCI registry
```console
helm install eg oci://docker.io/envoyproxy/gateway-helm -n envoy-gateway-system -f ./eg-values.yaml --create-namespace
```

3. Wait for Envoy Gateway to become available
```console
kubectl wait --timeout=5m -n envoy-gateway-system deployment/envoy-gateway --for=condition=Available
```

4. Create the GatewayClass CR
```console
kubectl apply -f ./gateway-class.yaml
```

5. Create ns 'gateway' for public use
```console
kubectl create namespace gateway
```

6. Add a label for the namespace being used.
```console
kubectl label namespace wh gateway=eg-public
```

7. Use the example directory to create examples  

8. Get the nodeport of gateway 'eg-public' and use it in the following browser access
```console
kubectl get svc -n envoy-gateway-system |grep 'eg-public'
```

9. Use a browser to access the address http://node-ip:32749/nginx-eg