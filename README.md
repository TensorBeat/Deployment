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
