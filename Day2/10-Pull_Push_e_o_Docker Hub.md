# Pull, Push e o Docker Hub

<br>

Um **Registry** de imagem é um local centralizado para armazenar e compartilhar imagens de container. Pode ser público ou privado. Docker Hub é um registro público que qualquer pessoa pode usar e é o registro padrão.

<br>

# Docker Pull 

Faz o download de imagens de um Registry

```shell
docker pull nome_da_imagem:tag
```

<br>

# Docker Login e Logout

```shell
docker login -u <usuário>
```
Será solicitado o `password` do usuário onde pode ser usado o token do usuário em seu lugar.

<br>

Para fazer o logout do usuário

```shell
docker logout
```

<br>

# Docker Push 

<br>

Para fazer o **Push** de uma imagem, ou seja, enviá-la para o Docker Hub (ou para outro Registry), o nome da imagem deve ter o seguinte padrão: `nome_do_usuario/nome_da_imagem:tag`.

Neste exemplo, iremos renomear a imagem abaixo `meu-nginx:1.0` para poder enviá-la para o Docker Hub.

```shell
docker image ls
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
meu-nginx    1.0       64a8046646fb   25 hours ago   16.9MB
```

Obs.: O `docker login` já dever ter sido executado e o `nome_do_usuario` adicionado à imagem deve ser o mesmo que fez o login no Docker Hub.
 
<br> 

Use o comando abaixo para renomear a imagem

```shell
docker image tag meu-nginx:1.0 nome_do_usuario/meu-nginx:1.0
```

<br>

Resultado
```shell
docker image ls                                      
REPOSITORY           TAG       IMAGE ID       CREATED        SIZE
meu-nginx            1.0       64a8046646fb   25 hours ago   16.9MB
nome_do_usuario/meu-nginx   1.0       64a8046646fb   25 hours ago   16.9MB
```

<br>

Outra opção é quando fazer o build da imagem já usar o nome do usuário com o nome da imagem:

```shell
docker image build -t nome_do_usuario/meu-nginx:1.0 .
```

<br>

Para fazer o Docker Push:

```shell
docker push 
```