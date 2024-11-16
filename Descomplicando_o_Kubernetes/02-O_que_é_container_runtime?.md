# O que é um container runtime?[^1][^2]

O **Container Runtime** é um componente de nível inferior normalmente usado em um *Container Engine*, mas também pode ser usado manualmente para testes.

A implementação de referência do padrão de tempo de execução da *Open Containers Initiative (OCI)* é *runc*. Este é o ambiente de execução de container mais usado, mas existem outros ambientes de execução compatíveis com OCI, como *crun*, *railcar* e *katacontainers*, *Docker*, *CRI-O* e muitos outros Container Engines dependem do runc.

<br>

O **Container Runtime** vêm em duas formas:

- **High-level runtimes** (como containerd e CRI-O): fornecem funções que são executadas sobre o tempo de execução de baixo nível.

- **Low-level runtimes**: são responsáveis ​​por criar e executar containers. A sua principal tarefa é fornecer gerenciamento do ciclo de vida do contêiner. O **Low-level runtimes** implementam a especificação de tempo de execução fornecida pela OCI (Open Container Initiative) que visa fornecer padrões abertos para containers Linux. A implementação de referência padrão para  **Low-level runtimes** especificados pelo OCI é o *runc*.

<br>

O **Container Runtime** é responsável por:

- Consumir o ponto de montagem do container fornecido pelo Container Engine (também pode ser um diretório simples para teste)
- Consumir os metadados do container fornecidos pelo Container Engine (também pode ser um config.json criado manualmente para teste)
- Comunicação com o kernel para iniciar processos em containers (clonar chamada de sistema)
- Configurando *cgroups*
- Configurando a política SELinux
- Configurando regras do App Armor

<br>

Para fornecer um pouco de história, quando o *Docker Engine* foi criado, ele dependia do LXC como tempo de execução do container. Mais tarde, a equipe do Docker desenvolveu sua própria biblioteca chamada *libcontainer* para iniciar containers.

Esta biblioteca foi escrita em Golang e compilada nos *Docker Engine* originais. Finalmente, quando o OCI foi criado, o Docker doou o código *libcontainer* e o transformou em um utilitário independente chamado *runc*.

Agora, *runc* é a implementação de referência usada por outros Container Engine, como CRI-O. No nível mais baixo, isso fornece a capacidade de iniciar um container de forma consistente, independentemente do mecanismo do container.

*Runc* é um utilitário muito conciso e espera que um ponto de montagem (diretório) e metadados (config.json) sejam fornecidos a ele. Veja este tutorial para mais informações sobre *runc*.

Para uma compreensão ainda mais profunda, consulte Noções básicas sobre os padrões de containers.

<br>

## Containerd[^3]

o **containerd** é uma abstração dos recursos de kernel de baixo nível usados ​​para executar e gerenciar containers em um sistema. É uma plataforma usada em software de contêiner como Docker e Kubernetes.

O Docker Engine usa **containerd** para gerenciamento do ciclo de vida de containers, que inclui criar, iniciar e parar containers. 

Por padrão, o **containerd** usa *runc* como tempo de *Container Runtime*.

<br>

## Fontes
[^1]: [Red Hat: A Practical Introduction to Container Terminology](https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction#basic_vocabulary)
[^2]: [AWS: Container runtime](https://docs.aws.amazon.com/whitepapers/latest/containers-on-aws/key-considerations.html#container-runtime)   
[^3]: [Docker: Alternative container runtimes](https://docs.docker.com/engine/daemon/alternative-runtimes/)   

