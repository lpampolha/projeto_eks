O projeto é de uma aplicação onde é possível gerar senhas, com um banco Redis, Ingress e certificado Let's Encrypt.

#### Subindo o EKS com eksctl

#eksctl create cluster --name=eks1 --version=1.24 --region=us-east-1 --nodegroup-name=eks-cluster-nodegroup --node-type=t3.medium --nodes=2 --nodes-min=1 --nodes-max=3 --managed

#### Deployando o Ingress Nginx Controller no EKS

Página oficial de guia para a instalação:
https://kubernetes.github.io/ingress-nginx/deploy/#aws

Para instalar, devemos fazer os seguintes passos:

- Deployar no EKS 

#kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.10.1/deploy/static/provider/aws/deploy.

- Verificando se tudo foi deployado
#kubectl get pods -n ingress-nginx

- Verificando o endereço do Ingress
#kubectl get svc -n ingress-nginx

- Verificando logs do Ingress Controller
#kubectl logs -f -n ingress-nginx ingress-nginx-controller-b6b99dbhhshad9-sbpljiuaxr

#### Deploy da aplicação de exemplo

    -app-deployment.yaml
    -app-service.yaml
    -redis-deployment.yaml
    -redis-service.yaml

#### Criando o recurso de Ingress

    -ingress.yaml

#### Cert-Manager
O Cert-Manager é um gerenciador de certificados 

Página oficial para instalação
https://cert-manager.io/docs/tutorials/

#### Instalando e configurando o Cert-Manager
#kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.15.1/cert-manager.yaml

- Verificando pods do cert-manager
#k get po -n cert-manager

- Verificando tudo com o ns cert-manager
#k get all -n cert-manager

#### Aplicando os issuers

  #staging_issuer.yaml
  #production_issuer.yaml

- Verificando os issuers
#kubectl get issuers.cert-manager.io
#kubectl get clusterissuers.cert-manager.io

#### Configurando o Ingress para usar o Cert-Manager

Adicionando annotation, apontando para o cert-manager

  -ingress-eks.yaml

Agora temos o Ingress com certificado