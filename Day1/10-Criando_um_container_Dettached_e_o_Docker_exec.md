# Criando um container Dettached e o Docker exec

<br>

## Docker Exec

O comando `docker container exec` executa um novo comando em um container em execução.

```shell
docker container exec <id ou nome do container> ls /usr/share/
```

<br>

Como acessar um container usando o Docker exec:

```shell
docker container exec -ti <id ou nome do container> bash
```
- `t`: Pseudo-TTY, abre um terminal
- `i`: Permite a interatiidade.
- `bash`: Abre o Shell do container. Às vezes, dependendo do sistema operacional do container, o `sh` é usado em seu lugar.

<br> 

## Alterar o conteúdo de um arquivo dentro de um container usando o Docker exec

Neste exemplo, será alterado o conteúdo do arquivo `index.html` usando o docker exec:
```shel
ddocker container exec meu-nginx sh -c "echo 'Toto is Lindo' > /usr/share/nginx/html/index.html"
```
- `meu-nginx`: Container onde será alterado o arquivo.
- `sh -c "echo 'Toto is Lindo' > /usr/share/nginx/html/index.html"`: Comando executado dentro do container que irá alterar o conteúdo do arquivo.

<br>

## Fazer o download de uma imagem do Docker Hub

Para fazer somente o download de uma imagem do Docker Hub sem criar um container.

```shell
docker image pull <nome da imagem:tag>
```
Se não colocar a tag será realizado o download da versão `latest` que é a última versão disponibilizada da imagem.

<br>

## Criar um container mas não colocá-lo em execução

Com o comando `docker container create` é possível somente criar um container sem executá-lo de imediato.
```shell
docker container create --name <nome do container> <image do container:tag> 
```