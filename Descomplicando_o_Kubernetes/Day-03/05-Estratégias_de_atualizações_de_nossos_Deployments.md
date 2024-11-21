# Estratégias de atualizações de nossos Deployments

Você pode especificar qual o tipo de estratégia será usada para trocar Pods antigos por novos. 

Pode ser configurada dois tipos de estratégias: **Rolling Update** e **Recreate**.

**RollingUpdate** é o valor padrão.

<br>

## Estratégia Rolling Update

A Deployment atualiza os Pods de forma contínua. Você pode especificar **maxUnavailable** e **maxSurge** para controlar o processo de atualização contínua.

<br>

### Max Unavailable

**maxUnavailable** é um campo opcional que especifica o número máximo de Pods que podem ficar indisponíveis durante o processo de atualização.

O valor pode ser um número absoluto (por exemplo, 5) ou uma porcentagem dos Pods desejados (por exemplo, 10%). O número absoluto é calculado a partir da porcentagem por arredondamento para baixo. O valor não poderá ser 0 se **maxSurge** for 0.

O valor padrão é 25%.

Por exemplo, quando esse valor é definido como 30%, o antigo ReplicaSet pode ser reduzido para 70% dos Pods desejados imediatamente quando a atualização contínua for iniciada.

Assim que os novos Pods estiverem prontos, o *ReplicaSet* antigo poderá ser reduzido ainda mais, seguido pelo aumento do novo *ReplicaSet*, garantindo que o número total de Pods disponíveis em todos os momentos durante a atualização seja de pelo menos 70% dos Pods desejados.

<br>

### Max surge

**MaxSurge** é um campo opcional que especifica o número máximo de Pods que podem ser criados além do número desejado de Pods.

O valor pode ser um número absoluto (por exemplo, 5) ou uma porcentagem dos Pods desejados (por exemplo, 10%). O valor não pode ser 0 se **MaxUnavailable** for 0. O número absoluto é calculado a partir da porcentagem por arredondamento.

O valor padrão é 25%.

Por exemplo, quando esse valor é definido como 30%, o novo *ReplicaSet* pode ser ampliado imediatamente quando a atualização contínua é iniciada, de modo que o número total de Pods novos e antigos não exceda 130% dos Pods desejados. 

Depois que os Pods antigos forem eliminados, o novo *ReplicaSet* poderá ser ampliado ainda mais, garantindo que o número total de Pods em execução a qualquer momento durante a atualização seja de no máximo 130% dos Pods desejados.

<br>

### Exemplos

Manifesto com o campo `strategy` configurado como `RollingUpdate`. 

Com o campo `maxUnavailable` configurado como `2`, significa que os Pods serão atualizados 02 de cada vez.

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
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
        - image: nginx:1.16.0
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

Verificar o status da estratégia

```shell
kubectl rollout status deployment -n webserver01 nginx-deployment
```

<br>

## Estratégia Recreate

A estratégia **Recreate** elimina todos os Pods antes que os novos Pods sejam criados.

<br>

>[!Note]
Isso garantirá apenas o encerramento do Pod antes da criação dos upgrades. Se você atualizar um *Deployment*, todos os pods da revisão antiga serão encerrados imediatamente.
A remoção bem-sucedida é aguardada antes que qualquer Pod da nova revisão seja criado.
Se você excluir manualmente um Pod, o ciclo de vida será controlado pelo *ReplicaSet* e o substituto será criado imediatamente (mesmo que o Pod antigo ainda esteja no estado Terminating).

### Exemplos

Manifesto com o campo `strategy` configurado como `Recreate`. 

Com o campo `maxUnavailable` configurado como `2`, significa que os Pods serão atualizados 02 de cada vez.

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
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
        - image: nginx:1.16.0
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

Verificar o status da estratégia

```shell
kubectl rollout status deployment -n webserver01 nginx-deployment
```

<br>

## Saiba mais
[Kubernetes: Deployments strategy](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#strategy)