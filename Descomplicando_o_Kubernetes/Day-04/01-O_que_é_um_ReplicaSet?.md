# O que é um ReplicaSet

O objetivo do ReplicaSet é manter um conjunto estável de réplicas de Pods em execução em qualquer momento. 

No entanto, um *Deployment* é um conceito de nível superior que gerencia ReplicaSets e fornece atualizações declarativas para Pods junto com muitos outros recursos úteis.

Portanto, recomendamos usar *Deployments* em vez de usar diretamente ReplicaSets, a menos que você precise de orquestração de atualização personalizada ou não precise de nenhuma atualização.

Na verdade, isso significa que talvez você nunca precise manipular objetos **ReplicaSet**: use um *Deployment* e defina seu aplicativo na seção *spec*.

<br>

## Saiba mais
[Kubernetes: ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)