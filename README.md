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
kubectl apply -f namespace.yml
```
O estágio anterior pode ser substituído pelo comando abaixo.
```sh
kubectl create namespace labwordpress
```
Listar *namespaces*.
```sh
kubectl get namespace
```
Aplicar arquivo de criação do *service*.
```sh
kubectl apply -f mysql-service.yml
```
Listar *services* do *namespace* **labwordpress**.
```sh
kubectl get service -n labwordpress
```
