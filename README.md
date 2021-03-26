# Deployment

Top level TensorBeat deployment on kubernetes

# Extras

Installs for things that aren't explicit in kubernetes folder

## Istio

Installed via GKE toggle  
Sidecar Toggle

```sh
kubectl label namespace default istio-injection=enabled --overwrite
```

## Helm installs (eventually automate these)

Dask

```sh
kubectl create namespace dask-gateway
helm repo add daskgateway https://dask.org/dask-gateway-helm-repo/
helm repo update
helm upgrade --install --namespace dask-gateway --version 0.9.0 --values ./kubernetes/dask/helm-values.yml dask-gateway daskgateway/dask-gateway
```

cert-manager

```sh
kubectl create namespace cert-manager
helm repo add jetstack https://charts.jetstack.io
helm install cert-manager jetstack/cert-manager --namespace cert-manager --version v1.2.0 --set installCRDs=true
```

kubeapps

```sh
kubectl create namespace kubeapps
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install kubeapps --namespace kubeapps bitnami/kubeapps
kubectl create --namespace default serviceaccount kubeapps-operator
kubectl create clusterrolebinding kubeapps-operator --clusterrole=cluster-admin --serviceaccount=default:kubeapps-operator
./getKubeappsToken.cmd
```
