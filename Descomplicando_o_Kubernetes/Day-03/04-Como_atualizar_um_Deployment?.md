# Como atualizar um Deployment?

<br>

Criar um Namespace chamado `nome-namespace`

```shell
kubectl create namespace nome-namespace
```

<br>

Manifesto de um Deployment com o campo Namespace de valor `webserver01` e 10 réplicas

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
  namespace: webserver01
spec:
  replicas: 10
  selector:
    matchLabels:
      app: nginx-deployment
  strategy: {}
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
        - image: nginx:1.15.0
          name: nginx
          resources:
            limits:
              cpu: 0.5
              memory: 256Mi
            requests:
              cpu: 0.3
              memory: 64Mi
```

<br>

Visualizar Deployments com o Namespace `webserver01`

```shell
kubectl get deployments -n webserver01 
```

<br>

Visualizar Pods com o Namespace `webserver01`

```shell
kubectl get pods -n webserver01 
```

<br>

Visualizar ReplicaSets com o Namespace `webserver01`

```shell
kubectl get replicaset -n webserver01 
```