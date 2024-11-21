# O que é um container engine?

Um **container engine** é um software que aceita solicitações do usuário, incluindo opções de linha de comando, extrai imagens e, da perspectiva do usuário final, executa o container.

Existem muitos **container engine**, incluindo *docker*, *RKT*, *CRI-O* e *LXD*. Além disso, muitos provedores de nuvem, plataformas como serviço (PaaS) e plataformas de container têm seus próprios mecanismos de container integrados que consomem imagens de container compatíveis com Docker ou OCI.

Ter um formato de imagem de container padrão do setor permite a interoperabilidade entre todas essas plataformas diferentes.

Indo mais fundo, a maioria dos **containers engine** não executa os containers, eles dependem de um tempo de execução compatível com OCI, como o *runc*. 

<br>

Normalmente, o **container engine** é responsável:

- Tratamento da entrada do usuário
- Tratamento de entrada por meio de uma API geralmente de um Container Orchestrator
- Download das imagens do container de um repositório (Registry)
- Expandir e descompactar a imagem do container no disco usando um *Graph Driver* (bloco ou arquivo dependendo do driver)
- Preparar um ponto de montagem de container, normalmente em armazenamento de cópia na gravação (novamente bloco ou arquivo dependendo do driver)
- Preparar os metadados que serão passados ​​para o container Container Runtime para iniciar o container corretamente
    - Usar alguns padrões da imagem do container (ex.ArchX86)
    - Usar a entrada do usuário para substituir padrões na imagem do container (por exemplo, CMD, ENTRYPOINT)
    - Usar padrões especificados pela imagem do container (ex. regras SECCOM)
- Chamar o *Container Runtime*

<br>

## Docker Engine

**Docker Engine** é uma tecnologia de conteinerização de código aberto para construir e conteinerizar seus aplicativos.

<br>

**Docker Engine** atua como um aplicativo cliente-servidor com:

- Um servidor com um processo daemon de longa duração `dockerd`.
- APIs que especificam interfaces que os programas podem usar para conversar e instruir o Docker daemon.
- Uma Interface de Linha de Comando (CLI) `docker`.


A CLI usa APIs do Docker para controlar ou interagir com o daemon do Docker por meio de scripts ou comandos diretos da CLI. Muitos outros aplicativos Docker usam a API e CLI subjacentes. O daemon cria e gerencia objetos Docker, como imagens, containers, redes e volumes.

Para obter mais detalhes, consulte Arquitetura Docker.

<br>

## Saiba mais
[Red Hat: A Practical Introduction to Container Terminology](https://developers.redhat.com/blog/2018/02/22/container-terminology-practical-introduction#basic_vocabulary)   
[Docker: Docker Engine](https://docs.docker.com/engine/)   

