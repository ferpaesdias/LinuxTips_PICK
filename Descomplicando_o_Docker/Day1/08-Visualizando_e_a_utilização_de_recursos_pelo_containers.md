# Visualização de métricas e recursos pelo container

<br>

## Docker Stats

O comando docker stats mostra a estatístida de dados dos containers em execução de forma dinâmica. Para interromper pressione `CTRL + C`.
 
```shell
docker container stats
```
 <br>

Saída do comando:
```shell
CONTAINER ID   NAME      CPU %     MEM USAGE / LIMIT   MEM %     NET I/O   BLOCK I/O   PIDS
4923ae583ef7   toskao3   0.00%     912KiB / 7.755GiB   0.01%     0B / 0B   0B / 0B     1
e43d7aff843e   toskao2   0.00%     912KiB / 7.755GiB   0.01%     0B / 0B   0B / 0B     1
```

<br>

## Docker top

<br>

Mostra os processos em execução de um container.

```shell
docker container top <id ou nome do container>
```

<br>


## Docker logs

<br>

Mostra os logs de um container.

```shell
docker container logs -f <id ou nome do container>
```
- `-f`: Mostra as últimas alterações conforme forem acontecendo.
