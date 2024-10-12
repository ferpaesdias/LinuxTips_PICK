# Visualizando e inspecionando imagens e containers

<br>

## Listando imagens

o comando abaixo é usado para listar imagens.
```shell
docker image ls
```

<br>

## Removendo uma imagem

o comando abaixo é usado para remover uma imagem. Só é possível remover uma imagem quando ela não está em uso por um container.

```shell
docker image rm <id da imagem>
```

<br>

## Inspecionando um container ou uma imagem

Mostra detalhes de um container

```shell
docker container inspect <nome ou id do container>
```

<br>

Mostra detalhes de uma imagem

```shell
docker image inspect <id da imagem>
```