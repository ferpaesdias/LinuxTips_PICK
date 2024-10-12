# Criando e gerenciando os primeiros containers

<br>

## Executar e remover containers 

Executar um container com a imagem do Ubuntu e já acessa o seu terminal shell
```shell
docker container run -it ubuntu
```
- `-i`: mantém o STDIN aberto e deixa você enviar o dados para o container através do input stardard.
- `-t`: Pseudo-TTY. Conecta seu terminal I/O stream (geralmente bash) ao container.     

<br> 

Neste caso, se sair do container usando o comando `exit` ou pressionando `CTRL + D` a execução do container é encerrada. Para sair do container sem encerrá-lo use o atalho `CTRL + P, Q`.

<br>

Listar os containers 
```shell
docker container ls -a
```
- `-a`: Inclui os containers que não estão em execução.

<br>

Saída do comando
```shell
# docker container ls -a          
CONTAINER ID   IMAGE         COMMAND       CREATED             STATUS                           PORTS     NAMES
b8bda2fbec56   hello-world   "/hello"      4 seconds ago       Exited (0) 2 seconds ago                   objective_feistel
513973ac410b   ubuntu        "/bin/bash"   About an hour ago   Up About an hour                           silly_blackwell
```

<br>

Acessar um container que está em execução. Se sair do container usando o comando `exit` ou pressionando `CTRL + D` a execução do container é encerrada. 
```shell
docker container attach 513973ac410b
```
- `513973ac410b`: id do container em execução

**Obs**.: Ao invés do *ID* também é possível usar o *nome do container*.

<br>

Remover um container que não está em execução.
```shell
docker container rm <nome ou ID do Container>
```

<br>

Remover um container que está em execução.
```shell
docker container rm -f <nome ou ID do Container>
```

<br>

## Iniciar e parar a execução de containers

<br>

Iniciar a execução um container que esta parado
```shell
docker container start <nome ou ID do Container>
```

<br>

Parar a execução de um container
```shell
docker container stop <nome ou ID do Container>
```

<br>

## Pausar e despausar a execução de um container

<br>

Pausar a execução um container que esta parado.
```shell
docker container pause <nome ou ID do Container>
```

<br>

Despausar a execução de um container.
```shell
docker container unpause <nome ou ID do Container>
```
