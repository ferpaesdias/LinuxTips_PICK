# Dockerfile e o Entrypoint

<br>

```Dockerfile
# Imagem que será a base desta imagem
FROM ubuntu:22.04

# Metadata sobre o container
LABEL maintainer="author@gmail.com"

# Executa um comando na durante a criação da imagem
RUN apt update && apt install -y nginx && rm -rf /var/lib/apt/list/*

# Mostra a porta que será exposta
EXPOSE 80

# Copia diretórios e arquivos do host para a imagem
COPY index.html /var/www/html/

# Altere o diretório de trabalho.
WORKDIR /var/www/html/

# Define variáveis de ambiente
ENV APP_VERSION=1.0.0

# Principal processo do container
ENTRYPOINT ["nginx"]

# Parâmetros do processo executado pelo Entrypoint
CMD ["-g", "daemon off;"]
```