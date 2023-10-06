Vamos usar o k3d derivado do k3s que é uma versão minimalista do kunernetes feito pelo pessoal do Rancher.

k3d.io
Instalação do k3d:
wget -q -O - https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash

Criação do cluster:
k3d cluster create -p "8000:30000@loadbalancer" --agents 2
Obs: Eu consigo fazer a mesma coisa com o kind

kubectl cluster-info
kubectl config use-context k3d-k3s-default
kubectl get nodes

Instalação do Istio
curl -L https://istio.io/downloadIstio | sh -
cd istio-1.19.0
mover para o opt com o sudo e colocar no path

Instalando com o profile default
istioctl install

kubectl get pods -> Não deve aparecer nada
kubectl get ns
kubectl get pod -n istio-system
kubectl get svc
kubectl get svc -n istio-system

-------------------------------
Injetando sidecar proxy
kubectl apply -f deployment.yaml 
kubectl delete -f deployment.yaml 
kubectl apply -f deployment.yaml 

kubectl label namespace default istio-injection=enabled

kubectl delete deploy nginx
kubectl apply -f deployment.yaml 
kubectl get pods
kubectl describe pod nginx-6c9d4d964d-9zvq4
-------------------------------------
Configurando addons - Kiali
kubectl apply -f addons/prometheus.yaml
kubectl apply -f addons/kiali.yaml
kubectl apply -f addons/jaeger.yaml
kubectl apply -f addons/grafana.yaml

kubectl get pod -n istio-system

kubectl logs pod/jaeger-db6bdfcb4-rl8rp --namespace=istio-system --container=jaeger --since=0

kubectl delete -f addons/jaeger.yaml
-- Problemas de memória
kubectl apply -f addons/jaeger.yaml

istioctl dashboard kiali
