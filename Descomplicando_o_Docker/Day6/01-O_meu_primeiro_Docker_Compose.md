# O meu primeiro Docker Compose

<br>

A propriedade `version` qual é a versão mais recente e recomendada do formato do arquivo Compose.

O Docker Compose não usa mais a propriedade `version` para selecionar um esquema exato para validar o arquivo do Compose, mas prefere o esquema mais recente quando ele é implementado.

<br>

### Criar o arquivo `docker-compose.yaml`

Normalmente, o Docker Compose a configuração de Docker Compose fica dentro do seguinte arquivo: `docker-compose.yaml`. Crie o arquivo com a seguinte configuração:

```docker
services:
  nginx:
    image: nginx:latest
    ports:
    - "8080:80/tcp"

```
- `services` : Se refere a componentes isolados da aplicação que definem contêineres e suas configurações, como imagem, volumes e redes.
- `nginx`: Nome do serviço.
- `image`: Nome da image mais a tag. Se não especificar a tag será utilizada a tag **latest**.
- `ports` (HOST:CONTAINER): Define o mapeamento de portas usadas entre o host e o container.  

<br>

### Executando o Docker Compose

No mesmo diretório que está o arquivo `docker-compose.yaml` digite o comando abaixo:

```shell
docker compose up -d
```
- `up`: Inicia todos os serviços (containers) que estão no arquivo `docker-compose.yaml`.
- `-d`: Inicia os serviços em segundo plano (background).

<br>

### Desativando os containers do Docker Compose

No mesmo diretório que está o arquivo `docker-compose.yaml`, execute o comando abaixo para *parar* e *remover* os **containers**, **networks**, **volumes** e **imagens** que foram criados pelos comando `docker compose up`.

```shell
docker compose down
```
<br>

### Listando os containers do Docker Compose

No mesmo diretório que está o arquivo `docker-compose.yaml`, execute o comando abaixo para *listar* os containers, que foram criados pelos comando `docker compose up`, que estão em execução.

```shell
docker compose ps
```
<br>

### Pausar e despausar os containers em Docker Compose

No mesmo diretório que está o arquivo `docker-compose.yaml`, execute o comando abaixo para *pausar* os containers, que foram criados pelos comando `docker compose up`, que estão em execução.

```shell
docker compose pause
```
<br>

Para *despausar* os containers:

```shell
docker compose unpause
```
<br>

