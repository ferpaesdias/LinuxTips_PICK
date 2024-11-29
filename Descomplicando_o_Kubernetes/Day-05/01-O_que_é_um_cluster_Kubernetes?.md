# O que é um cluster Kubernetes?

<br>

Um cluster Kubernetes consiste em um *Control Plane* mais um conjunto de *Workers*, chamadas *Nodes*, que executam aplicativos em containers. Cada cluster precisa de pelo menos um Node de Workers para executar Pods.

Os *Nodes* de Workers hospedam os Pods que são os componentes da carga de trabalho do aplicativo. O *Control Plane* gerencia os Nodes de Workers e os Pods no cluster. Em ambientes de produção, o *Control Plane* geralmente é executado em vários computadores e um cluster geralmente executa vários Nodes, proporcionando tolerância a falhas e alta disponibilidade.

<br>

## Saiba mais
[Kubernetes: Cluster Architecture](https://kubernetes.io/docs/concepts/architecture/)