# O meu primeiro Dockerfile

O nome do arquivo tem ser `Dockerfile`:

```Dockerfile
# Imagem que será a base desta imagem
FROM ubuntu:22.04

# Executa um comando na durante a criação da imagem
RUN apt update && apt install -y nginx && rm -rf /var/lib/apt/list/*

# Mostra a porta que será exposta
EXPOSE 80

# Executa o comando quando o container for executado
CMD ["nginx", "-g", "daemon off;"]
```

<br>

Para construir ou "buildar" a imagem execute o comando abaixo dentro do mesmo diretório do arquivo **Dockerfile**:

```shell
docker image build -t meu-nginx:1.0 .
```
- `-t`: Nome e, opcionalmente, uma tag no formato name:tag
- `.`: Significa o diretório de trabalho atual.