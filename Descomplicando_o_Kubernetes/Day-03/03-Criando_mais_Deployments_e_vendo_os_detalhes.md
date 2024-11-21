# Criando mais Deployments e vendo os detalhes

<br>

Para ver detalhes de um Deployment chamado `nginx-deployment`

```shell
kubectl describe deployments nginx-deployment
```

<br>

Criar um Deployment chamado `nginx-deployment` usando a linha de comando

```shell
kubectl create deployment --image nginx --replicas 3 nginx-deployment
```

<br>


Criar um arquivo YAML de um Deployment  `nginx-deployment` usando a linha de comando e a flag `--dry-run`

```shell
kubectl create deployment --image nginx --replicas 3 nginx-deployment --dry-run=client -o yaml > deployment.yaml
```

<br>

