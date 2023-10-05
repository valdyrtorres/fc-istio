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
