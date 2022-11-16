# Kubernetes - WordPress e MySQL
Documentação referente a aplicação das tecnologias WordPress e MySQL utilizando K8s.

## Documentação oficial
- [Kubernetes](https://kubernetes.io/docs/home/)

## Pré-requisitos
- Possuir o [Docker Desktop](https://docs.docker.com/get-docker/) instalado.

## Etapas da aplicação
Este tópico apresenta os estágios a ser seguidos para implementação.  
Aplicar arquivo para criação do *namespace*.
```sh
kubectl apply -f namespace.yaml
```
O estágio anterior pode ser substituído pelo comando abaixo.
```sh
kubectl create namespace labwordpress
```
Listar *namespaces*.
```sh
kubectl get namespace
```
Aplicar arquivos de criação dos *services*.
```sh
kubectl apply -f services/mysql-svc.yaml
```
```sh
kubectl apply -f services/wordpress-svc.yaml
```
Listar *services* do *namespace* **labwordpress**.
```sh
kubectl get service -n labwordpress
```
