# Diferentes formas de instalar um cluster Kubernetes

<br>

## Kubeadm

**Kubeadm** é uma ferramenta desenvolvida para fornecer `kubeadm init` e `kubeadm join` como "caminhos rápidos" de práticas recomendadas para a criação de clusters Kubernetes.

**Kubeadm** executa as ações necessárias para colocar um cluster mínimo viável em funcionamento. Por design, ele se preocupa apenas com a inicialização, não com o provisionamento de máquinas. Da mesma forma, a instalação de vários complementos interessantes, como o Kubernetes Dashboard, soluções de monitoramento e complementos específicos da nuvem, não está no escopo.

Em vez disso, esperamos que ferramentas de nível superior e mais personalizadas sejam construídas sobre o **kubeadm** e, idealmente, o uso do **kubeadm** como base de todas as implantações facilitará a criação de clusters compatíveis.

<br>

## Kubespray

**Kubespray** é uma combinação de Kubernetes e Ansible. Isso significa que podemos instalar o Kubernetes usando Ansible. Também podemos implantar clusters usando kubespray em serviços de computação em nuvem como EC2 (AWS).


Quais são os benefícios de usar o kubespray?

- Kubespray oferece flexibilidade de implantação. Ele permite implantar um cluster rapidamente e personalizar todos os aspectos da implementação.
- Kubespray encontra um equilíbrio entre flexibilidade e facilidade de uso.
- Você só precisa executar um manual do Ansible e seu cluster pronto para servir.

<br>

## kOps - Kubernetes Operations

O **kops** não apenas ajudará você a criar, destruir, atualizar e manter cluster Kubernetes de nível de produção e altamente disponível, mas também fornecerá a infraestrutura de nuvem necessária.

AWS (Amazon Web Services) e GCE (Google Cloud Platform) são atualmente oficialmente suportados, com DigitalOcean, Hetzner e OpenStack em suporte beta e Azure em alfa.

<br>

## minikube

**minikube** é o Kubernetes local, com foco em facilitar o aprendizado e o desenvolvimento para o Kubernetes.

Tudo que você precisa é de um contêiner Docker (ou compatível de forma semelhante) ou de um ambiente de máquina virtual, e o Kubernetes está a um único comando de distância: `minikube start`.

<br>

## kind

**kind** é uma ferramenta para executar clusters locais do Kubernetes usando “Nodes” de container Docker.

**kind** foi projetado principalmente para testar o próprio Kubernetes, mas pode ser usado para desenvolvimento local ou CI.

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
[Red Hat: An introduction to Kubespray](https://www.redhat.com/en/blog/kubespray-deploy-kubernetes)  
[Kubernetes SIGs: kOps - Kubernetes Operations](https://kops.sigs.k8s.io/)   
[Kubernetes SIGs: minikube](https://minikube.sigs.k8s.io/docs/)  
[Kubernetes SIGs: kind](https://kind.sigs.k8s.io/)  
[Amazon Docs: Amazon Elastic Kubernetes Service](https://docs.aws.amazon.com/whitepapers/latest/overview-deployment-options/amazon-elastic-kubernetes-service.html)    
[Microsoft Learn: O que é o AKS (Serviço de Kubernetes do Azure)?](https://learn.microsoft.com/pt-br/azure/aks/what-is-aks)     
[Google Cloud: Visão geral do GKE](https://cloud.google.com/kubernetes-engine/docs/concepts/kubernetes-engine-overview?hl=pt-br#whats_next)