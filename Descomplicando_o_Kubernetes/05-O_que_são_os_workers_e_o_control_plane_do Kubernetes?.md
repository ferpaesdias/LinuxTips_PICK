# O que são os workers e o control plane do Kubernetes?


Um cluster **Kubernetes** consiste em um **Control Plane** mais um conjunto de **Workers**, chamados **Nodes** (nós), que executam aplicativos em containers. Cada cluster precisa de pelo menos um node de Worker para executar **Pods**.

Os **Nodes Worker** hospedam os Pods que são os componentes do workload do aplicativo.

O **Control Plane** gerencia os Nodes Worker e os Pods em um Cluster. Em um ambiente de produção, o **Control Plane**, geralmente, é executado através de múltiplos computadores e um cluster, geralmente, executa múltiplos Nodes, proporcionando tolerância a falhas e alta disponibilidade.

<br>


