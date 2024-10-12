# Descomplicado o Dockerfile

```dockerfile
# Imagem que será a base desta imagem
FROM debian:11

# Executa um comando na durante a criação da imagem
RUN apt update && \
    apt install -y apache2 && \
    apt clean

# Define variáveis de ambiente
ENV APACHE_LOCK_DIR="/var/lock"
ENV APACHE_PID_FILE="/var/run/apache2.pid"
ENV APACHE_RUN_USER="www-data"
ENV APACHE_RUN_GROUP="www-data"
ENV APACHE_LOG_DIR="/var/log/apache2"

# Metadata sobre o container
LABEL description="Webserver"

# Define um volume a ser montado no container
VOLUME /var/www/html

# Mostra a porta que será exposta
EXPOSE 80

# Principal processo do container
ENTRYPOINT ["/us/sbin/apachectl"]

# Parâmetros do processo executado pelo Entrypoint
CMD ["-D", "FOREGROUND"]
```