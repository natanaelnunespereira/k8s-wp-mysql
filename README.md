<img src="https://github.com/kubernetes/kubernetes/raw/master/logo/logo.png" width="100"> <img src="https://user-images.githubusercontent.com/112975441/202521730-762beeae-fc01-4711-9657-fab46c3c486e.png" width="100"> <img src="https://user-images.githubusercontent.com/112975441/202522596-0dcacd65-ffb6-49fd-b7c7-474d8b03c355.png" width="100">

# Kubernetes - WordPress e MySQL
Documentação referente a aplicação das tecnologias WordPress e MySQL utilizando K8s.

## Documentação oficial
- [Kubernetes](https://kubernetes.io/docs/home/)

## Pré-requisitos
- Possuir o [Docker Desktop](https://docs.docker.com/get-docker/) instalado.

## Estrutura
Este tópico apresenta a descrição da estrutura do projeto.  
- [Namespace](/namespace/namespace.yaml): fornecer isolamento de recursos para o `labwordpress`.
- [Services](/services): expor a comunicação do cluster (`ClusterIP`, `NodePort` ou `LoadBalancer`).
- [Secrets](https://kubernetes.io/docs/concepts/configuration/secret/): contém dados confidenciais, por esse motivo não pode ser exposto neste repositório.
- [Volumes](/volumes): armazenar arquivos dos *containers*.
- [Deployments](/deployments): representar uma aplicação que será executada no *cluster*, podendo alterar a quantidade de réplicas simultâneas.  
- [Ingress](/ingress): expor rotas para fora do *cluster*.

## Etapas da aplicação
Este tópico apresenta os estágios a serem seguidos para implementação.  
- Aplicar arquivo para criação do *namespace*.
```sh
kubectl apply -f namespace/namespace.yaml
```
- O estágio anterior pode ser substituído pelo comando abaixo.
```sh
kubectl create namespace labwordpress
```
- Listar *namespaces*.
```sh
kubectl get namespace
```
- Aplicar arquivos de criação dos *services*.
```sh
kubectl apply -f services/mysql-svc.yaml
```
```sh
kubectl apply -f services/wordpress-svc.yaml
```
- Listar *services* do *namespace* **labwordpress**.
```sh
kubectl get svc -n labwordpress
```
- Modelo do arquivo secret.yaml.
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
- Aplicar arquivo *secret*.
```sh
kubectl apply -f secrets/secret.yaml
```
- Verificar *secret* do *namespace* **labwordpress**.
```sh
kubectl get secret -n labwordpress
```
- Aplicar arquivos de *PersistentVolumeClaim* (PVC).
```sh
kubectl apply -f volumes/mysql-pvc.yaml
```
```sh
kubectl apply -f volumes/wordpress-pvc.yaml
```
- Verificar a criação dos PVCs do *namespace* **labwordpress**.
```sh
kubectl get pvc -n labwordpress
```
- Aplicar arquivos de *deployment*.
```sh
kubectl apply -f deployments/mysql.yaml
```
```sh
kubectl apply -f deployments/wordpress.yaml
```
- Verificar *deployments* do *namespace* **labwordpress**.
```sh
kubectl get deployment -n labwordpress
```
- Aplicar arquivo do *ingress-controller* baseado no nginx.
```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.5.1/deploy/static/provider/cloud/deploy.yaml
```
- Verificar *pods* do *ingress*.
```sh
kubectl get pods -n ingress-nginx
```
- Aplicar arquivo do *ingress*.
```sh
kubectl apply -f ingress/wordpress-ingress.yaml
```
- Verificar *ingress* do *namespace* **labwordpress**.
```sh
kubectl get ingress -n labwordpress
```
- Listar recursos do *namespace* **labwordpress**.
```sh
kubectl get all -n labwordpress
```

### Acesso
- Alterar arquivo *hosts* adicionando linha contendo o IP do host e o host adicionado do Ingress.
```sh
C:\Windows\System32\drivers\etc\hosts
```
```sh
127.0.0.1    wordpress.compass.com
```
- Url *browser*: [wordpress.compass.com](http://wordpress.compass.com)
- *Container*.
```sh
kubectl exec -it <pod-name> -n labwordpress -- /bin/bash
```
- Verificar *logs*.
```sh
kubectl logs -f <pod-name> -n labwordpress
```
- Diretório dos volumes.
```sh
\\wsl$\docker-desktop-data\data\k8s-pvs
```

