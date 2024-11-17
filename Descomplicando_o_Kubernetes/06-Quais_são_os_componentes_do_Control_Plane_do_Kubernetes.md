# Quais são os componentes do Control Plane do Kubernetes[^1]

<br>

![Arquitetura Kubernetes ](./Imagens/kubernetes-cluster-architecture.svg)

<br>

Os componentes do **Control Plane** tem uma decisão global sobre o cluster (por exemplo, agendamento), assim como detectar e responder os eventos do cluster (por exemplo, inciar um novo Pod quando um campo de replicas de deploy não estiver satisfeito).

Os componentes do **Control Plane** podem ser executados em qualquer máquina do cluster. No entanto, para simplificar, os scripts de configuração normalmente iniciam todos os componentes do **Control Plane** em uma mesma máquina, e não executam os containers do usuário nesta máquina.

<br>

## kube-apiserver

O **API Server** é um componente que expõe a API do Kubernetes. O **API Server** é o front-end do *Control Plane* do Kubernetes.

A principal implementação de um servidor do Kubernetes API é o **kube-apiserver**.

O **kube-apiserver** foi profetado para escalar horizontalmente, isto é, ele escala implementando mais instâncias.

<br>

## etcd

Armazenamento de valor-chave consistente e altamente disponível usado como armazenamento do Kubernetes para todos os dados do cluster.

Se o seu cluster Kubernetes usar o **etcd** como armazenamento, certifique-se de ter um plano de backup para os dados.

O **etcd** armazena as informações do estado do cluster.

Somente o **kube-apiserver** se comunica com o **etcd**.

<br>

## kube-scheduler

O **kube-scheduler** é o componente do **Control Plane** que monitora Pods recém-criados sem Node atribuído e seleciona um Node para execução.

Os fatores levados em consideração nas decisões de agendamento incluem: requisitos de recursos individuais e coletivos, restrições de hardware/software/política, especificações de afinidade e antiafinidade, localidade de dados, interferência entre workloads e prazos.

<br>

## kube-controller-manager 

O **kube-controller-manager** é o componente do **Control Plane** que executa processos do controlador.

Logicamente, cada controlador é um processo separado, mas para reduzir a complexidade, todos eles são compilados em um único binário e executados em um único processo.

<br>

Existem muitos tipos diferentes de controladores. Alguns exemplos deles são:

- **Node Controller**: Responsável por perceber e responder quando os nós ficam inativos.

- **Job Controller**: monitora objetos de trabalho que representam tarefas únicas e, em seguida, cria Pods para executar essas tarefas até a conclusão.

- **EndpointSlice controller**: preenche objetos EndpointSlice (para fornecer um link entre serviços e Pods).

- **ServiceAccount controller**: crie ServiceAccounts padrão para novos namespaces.

A lista acima não é uma lista completa.

<br>

## cloud-controller-manager

O **cloud-controller-manager** é um componente do **Control Plane** do Kubernetes que incorpora lógica de controle específica da nuvem.

O **cloud-controller-manager** permite vincular seu cluster à API do seu provedor de nuvem e separa os componentes que interagem com essa plataforma de nuvem dos componentes que interagem apenas com seu cluster.

O **cloud-controller-manager** executa apenas controladores específicos do seu provedor de nuvem. Se você estiver executando o Kubernetes em suas próprias instalações ou em um ambiente de aprendizagem dentro de seu próprio PC, o cluster não possui um **cloud-controller-manager**.

Assim como acontece com o *kube-controller-manager*, o **cloud-controller-manager** combina vários loops de controle logicamente independentes em um único binário que você executa como um único processo. Você pode dimensionar horizontalmente (executar mais de uma cópia) para melhorar o desempenho ou ajudar a tolerar falhas.

<br>

Os seguintes controladores podem ter dependências de provedor de nuvem:

- **Node controller**: para verificar o provedor de nuvem para determinar se um nó foi excluído da nuvem depois de parar de responder

- **Route controller**: para configurar rotas na infraestrutura de nuvem subjacente

- **Service controller**: para criar, atualizar e excluir balanceadores de carga de provedor de nuvem

<br>

## Fontes
[^1]: [Kubernetes: Cluster Architecture](https://kubernetes.io/docs/concepts/architecture/)