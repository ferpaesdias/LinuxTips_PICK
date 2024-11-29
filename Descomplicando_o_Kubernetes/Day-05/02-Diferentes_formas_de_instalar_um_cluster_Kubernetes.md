# Diferentes formas de instalar um cluster Kubernetes

<br>

## Kubeadm

**Kubeadm** é uma ferramenta desenvolvida para fornecer `kubeadm init` e `kubeadm join` como "caminhos rápidos" de práticas recomendadas para a criação de clusters Kubernetes.

**Kubeadm** executa as ações necessárias para colocar um cluster mínimo viável em funcionamento. Por design, ele se preocupa apenas com a inicialização, não com o provisionamento de máquinas. Da mesma forma, a instalação de vários complementos interessantes, como o Kubernetes Dashboard, soluções de monitoramento e complementos específicos da nuvem, não está no escopo.

Em vez disso, esperamos que ferramentas de nível superior e mais personalizadas sejam construídas sobre o **kubeadm** e, idealmente, o uso do **kubeadm** como base de todas as implantações facilitará a criação de clusters compatíveis.

<br>

## Amazon Elastic Kubernetes Service - Amazon EKS

O **Amazon Elastic Kubernetes Service** (Amazon EKS) oferece flexibilidade para iniciar, executar e escalar aplicações do Kubernetes na nuvem ou on-premises. O Amazon EKS fornece clusters altamente disponíveis e seguros, enquanto automatiza tarefas importantes, como aplicação de patches, provisionamento de nós e atualizações.

<br>

## Azure Kubernetes Service - AKS

O **Azure Kubernetes Service** (AKS) é um serviço de Kubernetes gerenciado que você pode usar para implantar e gerenciar aplicativos conteinerizados. Você precisa de conhecimento mínimo de orquestração de container para usar o AKS.

O AKS reduz a complexidade e a sobrecarga operacional de gerenciar o Kubernetes passando grande parte dessa responsabilidade para o Azure.

O AKS é uma plataforma ideal para implantar e gerenciar aplicativos conteinerizados que exigem alta disponibilidade, escalabilidade e portabilidade e para implantar aplicativos em várias regiões, usando ferramentas de software livre e integração com ferramentas de DevOps existentes.

<br>

## Google Kubernetes Engine - GKE

O **Google Kubernetes Engine** (GKE) é uma implementação gerenciada pelo Google da plataforma de orquestração de containers de código aberto do Kubernetes. 

O GKE é ideal se você precisa de uma plataforma que permita configurar a infraestrutura que executa seus aplicativos conteinerizados, como rede, escalonamento, hardware e segurança. O GKE fornece a potência operacional do Kubernetes enquanto gerencia muitos dos componentes subjacentes, como o Control Plane e Nodes, para você.

<br>

## Saiba mais
[Amazon Docs: Amazon Elastic Kubernetes Service](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/amazon-elastic-kubernetes-service.html)    
[Microsoft Learn: O que é o AKS (Serviço de Kubernetes do Azure)?](https://learn.microsoft.com/pt-br/azure/aks/what-is-aks)     
[Google Cloud: Visão geral do GKE](https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview?hl=pt-br#whats_next)