# Buildando uma imagem de container com o Compose e aumentando o número de réplicas

<br>

### Fazendo o build de uma imagem usando o Docker Compose

```docker
services:
  name_service:
    build: ./caminho_Dockerfile

```
- `build`: Um caminho relativo para a pasta pai do arquivo Compose. Este caminho deve ser um diretório e conter um **Dockerfile**.

<br>


### Escalando a quantidade de réplicas de determinado serviço

No Docker Compose abaixo temos um servico appa e outro appb:

```docker
services:
  appa:
    image: appa:0.1
    networks:
      - net_exemplo

  appb:
    image: appb:0.1
    networks:
      - net_exemplo

networks:
  net_exemplo:
```
<br>

Podemos iniciar o Docker Compose acima com 03 réplicas do serviço **appa**. Para isso, execute o comando abaixo no mesmo diretório que está o arquivo `docker-compose.yaml`:

```shell
docker compose up -d --scale appa=3
```
**Obs**.: Não é possível escalar serviços que tenham portas publicadas (atributo `ports`) porque não pode haver mais de um container com a mesma porta publicada.