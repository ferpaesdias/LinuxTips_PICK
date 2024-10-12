# Transformando a nossa aplicação em uma imagem de container

<br> 

### Criando o Dockerfile

```dockerfile
FROM python:3.11

WORKDIR /app
COPY requirements.txt .
COPY app.py .
COPY templates templates/
COPY static static/

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000

CMD ["flask", "run", "--host=0.0.0.0"]
```

Obs.: Arquivo somente para consulta, não possui as dependências necessárias.

<br>

### Criando a imagem do App

```shell
docker image build -t giropops-senhas:1.0 .
```

<br>

### Executando o container do App

```shell
docker container run -d -e REDIS_HOST=<IP_DO_HOST> --name giropops-senhas -p 5000:5000 giropops-senhas:1.0
```

<br>

### Executando o container do Redis

```shell
docker container run -d --name redis -p 6379:6379 redis
```

