# Quais os componentes do Worker do Kubernetes?[^1]

<br>

![Arquitetura Kubernetes ](./Imagens/kubernetes-cluster-architecture.svg)

<br>

Os componentes do Node são executados em cada Node, mantendo os Pods em execução e fornecendo o ambiente de tempo de execução do Kubernetes.

<br>

## kubelet

O **kubelet** é um agente que é executado em cada cluster. Ele certifica que os containers estão sendo executados em um Pod.

O **kubelet** usa um conjunto de *PodSpecs* fornecidos por meio de vários mecanismos e garante que os containers descritos nesses *PodSpecs* estejam em execução e íntegros.

O **kubelet** não gerencia containers que não foram criados pelo Kubernetes.

<br>

## kube-proxy (Opcional)

O **kube-proxy** é um proxy de rede de cada Node em seu cluster, implementando parte do conceito de Kubernetes Service.

O **kube-proxy** mantém as regras de redes nos Nodes. Essas regras de rede permitem a comunicação de rede entre os seus Pods a partir de sessões de rede dentro ou fora do cluster.

O **kube-proxy** user a camada de filtragem de pacotes do sistema operacional, se houver uma e estiver disponível.

Se você usa um plugin de rede que implementa o encaminhamento de pacotes para serviços por si só e forneça um comportamento equivalente ao **kube-proxy**, não será necessário executar o **kube-proxy** em seu cluster.

<br>

## Container runtime

O **container runtime** é um componente fundamental que capacita o Kubernetes a executar containers de maneira eficaz. 

O **container runtime** é responsável por gerenciar a execução e o ciclo de vida dno ambiente Kubernetes. 

*O Kubernetes oferece suporte a **containers runtimes**, como containerd, CRI-O e qualquer outra implementação de Kubernetes CRI (Container Runtime Interface).

<br>

## Fontes
[^1]: [Kubernetes: Cluster Architecture](https://kubernetes.io/docs/concepts/architecture/)