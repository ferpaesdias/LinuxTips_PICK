# Conhecendo mais parâmetros no Dockerfile

<br>

```Dockerfile
# Imagem que será a base desta imagem
FROM ubuntu:22.04

# Executa um comando na durante a criação da imagem
RUN apt update && apt install -y nginx && rm -rf /var/lib/apt/list/*

# Mostra a porta que será exposta
EXPOSE 80

# Copia diretórios e arquivos do host para a imagem
COPY index.html /var/www/html/

# Executa o comando quando o container for executado
CMD ["nginx", "-g", "daemon off;"]

# Altere o diretório de trabalho.
WORKDIR /var/www/html/

# Define variáveis de ambiente
ENV APP_VERSION=1.0.0
```


