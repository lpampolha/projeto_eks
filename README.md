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