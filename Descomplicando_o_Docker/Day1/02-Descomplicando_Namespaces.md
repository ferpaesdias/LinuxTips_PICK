# Descomplicando Namespaces

*Namespaces* foram adicionados no kernel Linux na versão 2.6.24 e são eles que permitem o isolamento de processos quando estamos utilizando o Docker.

- **PID namespace**: Permite que cada container tenha seus próprios identificadores de processos.

- **Net namespace**: Permite que cada container possua sua interface de rede e portas. Para que seja possível a comunicação entre os containers, é necessário criar dois *Net Namespaces* diferentes, um reponsável pela interface do container (normalmente, chamada de eth0) e outro responsável por uma interface do host, normalmente chamada de veth* (veth + um identificador aleatório). Essas duas interfaces estão linkadas através da *bridge* *Docker0* no host, que permite a comunicação entre containers através de roteamento de pacotes.

- **Mnt namespace**: É a evolução do `chroot`. Permite que cada container possa ser o dono do seu ponto de montagem, bem como de seu sistema de arquivos raiz. Ele garante que um processo rodando em um sistema de arquivos não consiga acessar outro sistema de arquivos montado por outro *Mnt namespace*.

- **IPN namespace**: Provê um SYstemV IPC isolado, além de uma fila de mensagens POSIX própria.

- **UTS namespace**: Responsável por prover o isolamento de *hostname*, nome de domínio, versão de SO, etc.

- **User namespace**: Mantém o mapa de identificação de usuários em cada container.

<br>   

## Usando os Namespace em uma VM 

Ou, criando um container sem docker, só com Namespace.    
Executar os comandos abaixo em uma VM.

<br>   

### Instalação do debootstrap

```shell
apt-get install debootstrap -y
```

<br>

### Uso do debootstrap

O debootstrap faz o download de um sistema base de uma distribuição Linux em um diretório indicado no comando.

```shell
debootstrap stable /debian http://deb.debian.org/debian
```
- `stable`: Versão do Debian
- `/debian`: Diretório de destino
- `http://deb.debian.org/debian`: Endereço do repositório

<br>

### Comando unshare

O comando unshare executa um programa com alguns namespaces não compartilhados do processo pai.

```shell
unshare --mount --uts --ipc --net --map-root-user --user --pid --fork chroot /debian bash
```
- `--mount`: Descompartilha o namespace de montagens
- `--uts`: Descompartilha o namespace UTS (hostname, etc.)
- `--ipc`: Descompartilha o namespace de IPC de System V
- `--net`: Descompartilha o namespace de rede
- `--map-root-user`: mapeia usuário atual para root
- `--user`: Descompartilha o namespace do usuário
- `--pid`: Descompartilha o namespace do pid
- `--fork`: faz um fork antes de executar o <programa>
- `chroot /debian bash`: O chroot altera o diretório raiz do host para que os arquivos que estão no diretório */debian* quando executado pelo bash no ambiente isolado.

<br>

No ambiente isolado, para consequir visualizar os processos, é necessário montar o diretório `/proc`.

```shell
mount -t proc none /proc
```

<br>

Também é interessante montar os diretórios `/sys` e `/tmp` que são utilizados por sistemas Linux.

```shell
mount -t sysfs none /sys
mount -t tmpfs none /tmp
```

<br>

### Listar as Namespaces

No host, para listar as namespaces, use o comando `lsns`.
