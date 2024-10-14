# Criando um volume do tipo tmpfs

<br>

Um volume **tmpfs** é temporário e persiste apenas na memória do host. Quando o container para, a montagem **tmpfs** é removida e os arquivos gravados lá não serão persistidos.
Isso é útil para armazenar temporariamente arquivos confidenciais que você não deseja persistir no host ou na camada gravável do container.

<br>

## Limitações do volume tmpfs

- Não é possível compartilhar volumes **tmpfs** entre containers.
- O volume **tmpfs** só estará disponível se você estiver executando o Docker no Linux.
- Definir permissões em **tmpfs** pode fazer com que elas sejam redefinidas após a reinicialização do container. Em alguns casos, definir o uid/gid pode servir como uma solução alternativa.

<br>

## Executar um container com um volume tmpfs usando a flag `--mount`

<br>

Para montar o volume do tipo **tmpfs** não se usa a opção `source`.

```shell
docker container run -d --name container-teste --mount type=tmpfs,target=/app -p 8080:80 nginx
```
