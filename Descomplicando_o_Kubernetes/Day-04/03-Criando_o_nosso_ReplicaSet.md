# Criando o nosso ReplicaSet

<br>

Exemplo de *manifesto* do ReplicaSet

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  labels:
    app: nginx-app
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-app
  template:
    metadata:
      labels:
        app: nginx-app
    spec:
      containers:
      - name: nginx
        image: nginx:1.19.2
        resources:
          limits:
            cpu: 0.5
            memory: 256Mi
          requests:
            cpu: 0.3
            memory: 128Mi
```

<br>

>[!Note]
Não gerencie **ReplicaSets** diretamente, use sempre um **Deployment**.

<br>

Executar o *manifesto*

```shell
kubectl apply -f nome-manifesto.yaml
```

<br>

Após a execução do manifesto, se alterar algum campo em `spec.template.spec`, os Pods não serão atualizados automaticamente. Os Pods serão atualizados depois de encerrados manualmente.

<br>

## Saiba mais
[Kubernetes: ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)   