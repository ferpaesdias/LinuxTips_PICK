# Utilizando Volumes com o Docker Compose

<br>

Adicionando um volume no Docker Compose:

```docker
services:
  nginx:
    image: nginx:alpine3.20
    ports:
      - "8080:80/tcp"
    volumes:
      - nginx_html:/usr/share/nginx/html/

volumes:
  nginx_html:
    name: "nginx_html"
    external: true

```
- Na seção `volumes`, o atributo `name` é opcional.
- Na seção `volumes`, o atributo `external` configurado como `true` especifica que esse volume já existe na plataforma e seu ciclo de vida é gerenciado fora do aplicativo, portanto, o Docker Compose não cria o volume e retorna um erro se o volume não existir. A sua configuração padrão é `false`.