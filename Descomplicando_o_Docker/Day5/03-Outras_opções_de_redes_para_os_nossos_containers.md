# Outras opções de redes para os nossos containers

<br>

## Executar um container com um DNS personalizado

<br>

Executando um container com o DNS do Google
```shell
docker container run --dns 8.8.8.8 <nome_image:tag>
```

<br>

## Criar rede com um endereço de subrede e executar um container com um IP desta subrede

<br>

```shell
docker network create --subnet 192.0.2.0/24 network_exemplo
docker container run --network=network_exemplo --ip=192.0.2.254 <nome_image:tag>
```


