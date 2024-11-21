# Fazendo Rollback e conhecendo o comando Rollout

Às vezes, você pode desejar reverter uma implantação; por exemplo, quando a implantação não é estável.

Por padrão, todo o histórico de implementação do *Deployment* é mantido no sistema para que você possa reverter quando quiser (você pode alterar isso modificando o limite do histórico de revisões).

<br>

>[!Note]
Uma revisão de *Deployment* só é criada quando houver alteração em um template de um Pod, ou seja, dentro do campo `spec.template` de um manifesto de *Deployment*.   

<br>

Verificar o status de uma implementação

```shell
kubectl rollout status deployment -n webserver01 nginx-deployment
```

<br>

Verificar as revisões de um *Deployment*

```shell
kubectl rollout history deployment -n webserver01 nginx-deployment
```

<br>


Para verificar os detalhes de cada revisão de um *Deployment*

```shell
kubectl rollout history deployment -n webserver01 nginx-deployment --revision 3
```

<br>

Fazer um Rollback da revisão anterior

```shell
kubectl rollout undo deployment -n webserver01 nginx-deployment
```

<br>

Fazer o Rollback para uma versão específica

```shell
kubectl rollout undo deployment -n webserver01 nginx-deployment --to-revision 3
```

<br>

Verificar qual revisão está sendo utilizada, execute o comando `kubectl describe` e verifique o campo `Annotation`

```shell
kubectl describe deployments -n webserver01 nginx-deployment
```

<br>

Abaixo, a saída do comando mostra que está usando a revisão 5

```shell
Name:               nginx-deployment
Namespace:          webserver01
CreationTimestamp:  Thu, 21 Nov 2024 14:23:44 -0300
Labels:             app=nginx-deployment
Annotations:        deployment.kubernetes.io/revision: 5
Selector:           app=nginx-deployment
```

<br>

Ao atualizar um **Deployment**, ou planejar fazê-lo, você pode pausar os rollouts desse **Deployment** antes de acionar uma ou mais atualizações.

Quando estiver pronto para aplicar essas alterações, você retoma as distribuições do **Deployment**. Essa abordagem permite aplicar diversas correções entre a pausa e a retomada, sem acionar rollouts desnecessárias.

<br>

Pausar os rollouts. Marque os rollouts como *paused* para evitar rollouts questionáveis

```shell
kubectl rollout pause deployments -n webserver01 nginx-deployment
```
<br>

Retomar os rollouts marcados como *paused*

```shell
kubectl rollout resume deployments -n webserver01 nginx-deployment
```
<br>

Reiniciar um Deployment. Todos os Pods serão finalizados e iniciados conforme o manifesto do *Deployment*

```shell
kubectl rollout restart deployments -n webserver01 nginx-deployment
```
<br>

## Saiba mais
[Kubernetes: Deployments Updating a Deployment](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#updating-a-deployment)
