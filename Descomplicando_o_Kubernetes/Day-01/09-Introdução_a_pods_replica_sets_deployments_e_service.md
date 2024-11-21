# Introdução a pods, replica sets, deployments e service

<br>

## Pods

**Pods** são as menores unidades de computação ​​que você pode criar e gerenciar no Kubernetes.

Um **Pod** é um grupo de um ou mais containers, com armazenamento compartilhado e recursos de rede, e uma especificação de como executar os containers.

O conteúdo de um **Pod** é sempre colocado e agendado conjuntamente, e executado em um contexto compartilhado.

Um **Pod** modela um "host lógico" específico do aplicativo: ele contém um ou mais containers de aplicativos que são, relativamente, fortemente acoplados. Em contextos fora da nuvem, os aplicativos executados na mesma máquina física ou virtual são análogos aos aplicativos na nuvem executados no mesmo host lógico.

Além de containers de aplicativos, um **Pod** pode conter containers de inicialização executados durante a inicialização do **Pod**. Você também pode injetar containers temporários para depurar um **Pod** em execução.

<br>

## Deployments

Um **Deployment** gerencia um conjunto de Pods para executar um workload de aplicativo, geralmente uma que não mantém o estado.

Um **Deployment** fornece atualizações declarativas para Pods e ReplicaSets.

Você descreve um estado desejado em um **Deployment** e o controlador de **Deployments** altera o estado real para o estado desejado em uma taxa controlada.

Você pode definir **Deployments** para criar novos ReplicaSets ou para remover **Deployments** existentes e adotar todos os seus recursos com novas **Deployments**.

<br>

## Replica Set

O objetivo de um **ReplicaSet** é manter um conjunto estável de Pods em execução a qualquer momento. Como tal, é frequentemente utilizado para garantir a disponibilidade de um número específico de Pods idênticos.

Normalmente, você define um *Deployment* e permite que ele gerencie **ReplicaSets** automaticamente.

<br>

## Service

No Kubernetes, um **Serviço** é um método para expor um aplicativo de rede que está sendo executado como um ou mais Pods em seu cluster.

Um objetivo principal dos **Services** no Kubernetes é que você não precise modificar seu aplicativo existente para usar um mecanismo de descoberta de serviço desconhecido.

Você pode executar código em Pods, seja um código projetado para um mundo nativo da nuvem ou um aplicativo mais antigo que você "containerizou".

Você usa um **Service** para disponibilizar esse conjunto de Pods na rede para que os clientes possam interagir com ele.

<br>

## Saiba mais
[Kubernetes: Pods](https://kubernetes.io/docs/concepts/workloads/pods/)   
[Kubernetes: Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)   
[Kubernetes: ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/)   
[Kubernetes: Service](https://kubernetes.io/docs/concepts/services-networking/service/)   
