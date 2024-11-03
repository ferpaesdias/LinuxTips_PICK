# Limitando recursos como CPU e Memória

<br>

### Limitar um container para usar no máximo 0,5 CPU

<br>

```shell
docker container run --cpus 0.5 <nome_image:tag>
```
<br>


### Limitar um container para usar no máximo 64 MB de memória e 128 MB de memória swap

<br>

```shell
docker container run --memory 64m --memory-swap 128m <nome_image:tag>
```
<br>

