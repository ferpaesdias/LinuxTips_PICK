# Como instalar o Docker Engine no Linux

<br>

O Docker Engine é uma tecnologia de conteinerização responsável por construir e conteinerizar suas aplicações.   
Para fazer a instalação do Docker Engine em qualquer distribuição Linux é só executar o comando abaixo. Sempre será instalada a versão mais recente do Docker.

```shell
sudo curl -fsSL https://get.docker.com | bash
```

<br>

Execute o container abaixo para testar a instalação do Docker.
```shell
docker container run hello-world
```