# Criando uma Network e conectando nossos containers

<br>

Conectando 02 containers entre si.

Criando uma Network do tipo (driver) bridge:

```shell
docker network create --driver bridge network_exemplo
```
Não é necessário utilizar a flag `--driver` porque a opção driver é default.

<br>

Criando os containers usando a network criada anteriormente.

Container01:
```shell
docker container run -d --name container01 --network network_exemplo <nome_image:tag> 
```

<br>

Container02:
```shell
docker container run -d --name container02 --network network_exemplo <nome_image:tag> 