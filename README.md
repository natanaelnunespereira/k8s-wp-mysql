<img src="https://github.com/kubernetes/kubernetes/raw/master/logo/logo.png" width="100"> <img src="https://user-images.githubusercontent.com/112975441/202521730-762beeae-fc01-4711-9657-fab46c3c486e.png" width="100"> <img src="https://user-images.githubusercontent.com/112975441/202522596-0dcacd65-ffb6-49fd-b7c7-474d8b03c355.png" width="100">

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
kubectl get svc -n labwordpress
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
Aplicar arquivos de *deployment*.
```sh
 kubectl apply -f deployments/mysql.yaml
```
```sh
kubectl apply -f deployments/wordpress.yaml
```
Verificar *deployments* do *namespace* **labwordpress**.
```sh
kubectl get deployment -n labwordpress
```
Listar recursos do *namespace* **labwordpress**.
```sh
kubectl get all -n labwordpress
```

### Acesso
*Container*.
```sh
kubectl exec -it <pod-name> -n labwordpress -- /bin/bash
```
Verificar *logs*.
```sh
kubectl logs -f <pod-name> -n labwordpress
```
