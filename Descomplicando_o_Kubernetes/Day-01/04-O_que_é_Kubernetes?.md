# O que é Kubernetes?[^1]

**Kubernetes** é uma plataforma portátil, extensível e de código aberto para gerenciamento de cargas de trabalho e serviços em containers, que facilita a configuração declarativa e a automação.

Possui um ecossistema grande e em rápido crescimento. Os serviços, suporte e ferramentas do **Kubernetes** estão amplamente disponíveis.

<br>

## Por que você precisa do Kubernetes e o que ele pode fazer

**Kubernetes** fornece uma estrutura para executar sistemas distribuídos de forma resiliente. Ele cuida do dimensionamento e do failover do seu aplicativo, fornece padrões de implantação e muito mais. Por exemplo: o **Kubernetes** pode gerenciar facilmente uma implantação *canary* para o seu sistema.

<br>

**Kubernetes** fornece:

- **Descoberta de serviço e balanceamento de carga**: O **Kubernetes** pode expor um container usando o nome DNS ou seu próprio endereço IP. Se o tráfego para um container for alto, o **Kubernetes** será capaz de balancear a carga e distribuir o tráfego da rede para que a implantação seja estável.

- **Orquestração de armazenamento**: O **Kubernetes** permite montar automaticamente um sistema de armazenamento de sua escolha, como armazenamentos locais, provedores de nuvem pública e muito mais.

- **Rollouts e rollbacks automatizados**: Você pode descrever o estado desejado para o deploy de seus containers usando o **Kubernetes** e pode alterar o estado real para o estado desejado em uma taxa controlada. Por exemplo, você pode automatizar o **Kubernetes** para criar novos containers para seus deploys, remover containers existentes e adotar todos os seus recursos no novo container.

- **Empacotamento binário automático**: Você fornece ao **Kubernetes** um cluster de nós que pode ser usado para executar tarefas nos containers. Você informa ao **Kubernetes** quanta CPU e memória (RAM) cada container precisa. O **Kubernetes** pode acomodar containers em seus nós para fazer o melhor uso de seus recursos.

- **Autocorreção**: O **Kubernetes** reinicia containers que falham, substitui containers, elimina containers que não respondem à verificação de integridade definida pelo usuário e não os anuncia aos clientes até que estejam prontos para servir.

- **Gerenciamento de configuração e de segredos**: O **Kubernetes** permite armazenar e gerenciar informações confidenciais, como senhas, tokens OAuth e chaves SSH. Você pode implantar e atualizar segredos e configurações de aplicativos sem reconstruir as imagens de container e sem expor segredos da configuração da *stack*.

- **Execução em lote**: Além dos serviços, o **Kubernetes** pode gerenciar suas cargas de trabalho em lote e CI, substituindo containers que falham, se desejado.

- **Dimensionamento horizontal**: Aumente ou diminua seu aplicativo com um comando simples, com uma UI ou automaticamente com base no uso da CPU.

- **IPv4/IPv6 dual-stack**: Alocação de endereços IPv4 e IPv6 para pods e serviços.

- **Projetado para extensibilidade**: Adicione recursos ao seu cluster **Kubernetes** sem alterar o upstream do código-fonte.

<br>

## O que o Kubernetes não é

**Kubernetes** não é um sistema PaaS (Plataforma como Serviço) tradicional e completo. 

Como o **Kubernetes** opera no nível do container e não no nível do hardware, ele fornece alguns recursos geralmente aplicáveis, comuns às ofertas de PaaS, como deploys, escalonamento, balanceamento de carga, e permite que os usuários integrem suas soluções de registro, monitoramento e alertas. No entanto, o **Kubernetes** não é monolítico e essas soluções padrão são opcionais e conectáveis.

O **Kubernetes** fornece os blocos de builds para a build de plataformas de desenvolvedores, mas preserva a escolha e a flexibilidade do usuário onde for importante.

<br>

Kubernetes:

- **Não limita os tipos de aplicativos suportados**: O **Kubernetes** visa oferecer suporte a uma variedade extremamente diversificada de cargas de trabalho, incluindo cargas de trabalho stateless, statefull e de processamento de dados. Se um aplicativo puder ser executado em um contêiner, ele deverá funcionar perfeitamente no **Kubernetes**.

- **Não faz o deploy de seu código-fonte e não cria seu aplicativo**: Continuous Integration, Entrega, e Deployment (CI/CD) são determinados pelas culturas e preferências da organização, bem como pelos requisitos técnicos.

- **Não fornece serviços em nível de aplicativo, como middleware, frameworks de processamento de dados (por exemplo, Spark), bancos de dados, caches, nem sistemas de armazenamento de cluster (por exemplo, Ceph) como serviços integrados**: Esses componentes podem ser executados no **Kubernetes** e/ou acessados ​​por aplicativos executados no **Kubernetes** por meio de mecanismos portáteis, como o Open Service Broker.

- **Não determina soluções de registro, monitoramento ou alertas**: Fornece algumas integrações como prova de conceito e mecanismos para coletar e exportar métricas.

- **Não fornece nem exige uma linguagem/sistema de configuração (por exemplo, Jsonnet)**. Ele fornece uma API declarativa que pode ser alvo de formas arbitrárias de especificações declarativas.

- Não fornece nem adota nenhum sistema abrangente de configuração, manutenção, gerenciamento ou autocorreção da máquina.

- **O Kubernetes não é um mero sistema de orquestração**. Na verdade, elimina a necessidade de orquestração. A definição técnica de orquestração é a execução de um fluxo de trabalho definido: primeiro faça A, depois B e depois C. Em contraste, o **Kubernetes** compreende um conjunto de processos de controle independentes e combináveis ​​que conduzem continuamente o estado atual em direção ao estado desejado fornecido. Não importa como você vai de A a C. O controle centralizado também não é necessário. Isso resulta em um sistema mais fácil de usar e mais poderoso, robusto, resiliente e extensível.

<br>

## Fontes
[^1]: [Kubernetes: Overview](https://kubernetes.io/docs/concepts/overview/)