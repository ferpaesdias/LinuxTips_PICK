# Trabalhando com o tamanho e o número de camadas da imagem

<br> 

### Criando o Dockerfile

Alterando a imagem base `FROM` para a versão "slim".

```dockerfile
FROM python:3.11-slim

WORKDIR /app
COPY requirements.txt .
COPY app.py .
COPY templates templates/
COPY static static/

RUN pip install --no-cache-dir -r requirements.txt

EXPOSE 5000

CMD ["flask", "run", "--host=0.0.0.0"]
```

## Tamanho das imagens

```shell
docker image ls                            
REPOSITORY        TAG       IMAGE ID       CREATED          SIZE
giropops-senhas   2.0       e7f13a930bd0   2 minutes ago    148MB
giropops-senhas   1.0       bc2659c12d26   28 minutes ago   1.03GB
```
- `TAG 1.0`: Imagem padrão
- `TAG 2.0`: Imagem slim