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
Modelo do arquivo secret.yaml.
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysql-secret
  namespace: labwordpress
type: Opaque
data:
  mysql_root_password: <root-password>
  mysql_user: <user>
  mysql_password: <user-password>
```
Aplicar arquivo *secret*.
```sh
kubectl apply -f secrets/secret.yaml
```
Verificar *secret* do *namespace* **labwordpress**.
```sh
kubectl get secret -n labwordpress
```
Aplicar arquivos de *PersistentVolumeClaim* (PVC).
```sh
kubectl apply -f volumes/mysql-pvc.yaml
```
```sh
kubectl apply -f volumes/wordpress-pvc.yaml
```
Verificar a criação dos PVCs do *namespace* **labwordpress**.
```sh
kubectl get pvc -n labwordpress
```
