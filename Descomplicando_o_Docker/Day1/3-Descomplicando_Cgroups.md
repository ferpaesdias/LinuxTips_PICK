# Descomplicando Cgroups

<br>

### Instalação do cgroups-tools

Para manipular o Cgroups é necessário utilizar a ferramenta`cgroups-tools`

```shell
apt-get install cgroups-tools -y
```

<br>

Criando um novo Cgroup

```shell
cgcreate -g cpu,memory,blkio,devices,freezer:giropops
```

<br>

Lista os diretórios associados ao cgroup CPU Giropops

```shell
ls /sys/fs/cgroup/cpu/giropops/
```

<br>

Use o comando unshare para criar um ambiente isolado

```shell
unshare --mount --uts --ipc --net --map-root-user --user --pid --fork chroot /debian bash
```

<br>

Sem encerrar o ambiente isolado (abra outro terminal), no host, use o comando `ps -ef` para mostrar os processos em execução. Copie o PID do bash que está logo após o unshare. O processo pai desse *bash* é o próprio *unshare*.

```shell
root         19368     1845    0 07:44   pts/1    00:00:00  unshare --mount --uts --ipc ...
root         19369    19368    0 07:44   pts/1    00:00:00  bash
root         19374     1837    0 07:45   pts/1    00:00:00  ps -ef
```

<br>

### Adiciona o ambiente isolado ao Cgroup giropops

Usa o PID do bash copiado no passo anterior para adicionar o ambiente isolado ao Cgroup giropops.

```shell
cgclassify -g cpu,memory,blkio,devices,freezer:giropops 19369
```

<br>

### Especificar a quota de uso do CPU

Especifica a quota de uso de uso de CPU ao Cgroups giropops
```shell
cgset -r cpu.cfs_quota_us=1000 giropops
```

