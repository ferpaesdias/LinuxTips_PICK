# O Deployment e o ReplicaSet

Um **Deployment** fornece atualizações declarativas para **Pods** e **ReplicaSets**.

Você descreve um estado desejado em uma **Deployment** e o **Deployment Controller** altera o estado real para o estado desejado em uma taxa controlada. Você pode definir **Deployment** para criar novos **ReplicaSets** ou para remover **Deployments** existentes e adotar todos os seus recursos com novos **Deployments**.

<br>

>[!Note]
Não gerencie **ReplicaSets** pertencentes a um **Deployment**.

<br>

Listar os ReplicaSets

```shell
kubectl get replicaset
```

<br>

Saída do comando
```shell
NAME                          DESIRED   CURRENT   READY   AGE
nginx-deployment-6f86f979f5   1         1         1       21m
```

Observe que o nome do **ReplicaSet** é sempre formatado como `[NOME-DEPLOYMENT]-[HASH]`. Este nome se tornará a base para os Pods criados.


<br>

O nome dos Pods, quando criados usando um **Deployment**, é formatado como `[NOME-DEPLOYMENT]-[HASH-REPLICASET]-[HASH]`. Veja no exemplo abaixo a saída do comando `kubectl get pods`

```shell
NAME                                READY   STATUS    RESTARTS   AGE
nginx-deployment-6f86f979f5-qrrgw   1/1     Running   0          33m
```

<br>

## Saiba mais
[Kubernetes: Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)   
[Kubernetes: ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)   