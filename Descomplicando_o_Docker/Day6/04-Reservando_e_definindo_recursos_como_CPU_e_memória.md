# Reservando e definindo recursos como CPU e memória

<br>

Como definir a quantidade de **CPU** e **memória** no Docker Compose.

```docker
services:
  nginx:
    image: nginx:alpine3.20
    ports:
      - "8080:80/tcp"
    volumes:
      - nginx_html:/usr/share/nginx/html/
    deploy:
      resources:
        reservations:
          cpus: '0.25'
          memory: 128M
        limits:
          cpus: '0.5'
          memory: 256M

volumes:
  nginx_html:
    name: "nginx_html"
    external: true

```
- `deploys`: É uma parte opcional do Docker Compose. Ele fornece um conjunto de especificações de implantação para gerenciar o comportamento de containers em diferentes ambientes.
- `resources`: Configura restrições de recursos físicos para que o container seja executado na plataforma.
- `reservations`: Garante que o container possa alocar pelo menos a quantidade configurada.
- `limits`: Não será alocado mais recursos do que os valores estibulados neste atributo.
- `cpus`: Configura quantos recursos de CPU disponíveis, como número de núcleos, um container pode usar.
- `memory`: Configura uma quantidade de memória que um container pode alocar. As unidades suportadas são b (bytes), k ou kb (kilo bytes), m ou mb (mega bytes) e g ou gb (giga bytes).


<br>

## Iniciar um serviço somente após um outro serviço ter iniciado

<br>

No exemplo abaixo, o atributo `depends_on` informa que o serviço **appb** só ira iniciar quando o **appa** já estiver iniciado.

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
    depends_on:
      - appa

networks:
  net_exemplo:
```