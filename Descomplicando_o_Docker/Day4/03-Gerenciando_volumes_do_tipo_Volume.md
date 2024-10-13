# Gerenciando volumes do tipo Volume

<br>

### Listar volumes

```shell
docker volume ls
```

<br>

### Criar um Volume

```shell
docker volume create nome-volume
```

<br>

### Inspecionar um Volume

```shell
docker volume inspect nome-volume
```

<br>

### Executar um container montando um volume do tipo Volume

Se o volume não existir será criado um novo

```shell
docker container run -ti --name container-teste --mount type=volume,source=nome-volume,target=/app debian:11
```

<br>

### Apagar volumes que não estão em uso

```shell
docker volume prune
```