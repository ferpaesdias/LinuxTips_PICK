# Criando um Deployment através de um manifesto

<br>

## Manifesto

Manifesto que cria um Deployment de nome `nginx-deployment` que possui 03 réplicas de um container com a imagem do `nginx`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
spec:
  replicas: 3
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
      - image: nginx
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

## Comandos

Iniciar o Deployment via Manifesto

```shell
kubectl apply -f deployment.yaml
```

<br>

Listar os Deployments

```shell
kubectl get deployments
```

<br>

Listar todos os Pods com uma determinada label

```shell
kubectl get pods -l app=nginx-deployment
```

<br>

## Saiba mais
[Kubernetes: Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment)