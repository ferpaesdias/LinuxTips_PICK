# O Multistage no Dockerfile

<br>

```dockerfile
FROM golang:1.18 AS builder
WORKDIR /app
COPY hello.go ./
RUN go mod init hello
RUN go build -o /app/hello

FROM alpine:3.20
COPY --from=builder /app/hello /app/hello
CMD ["/app/hello"]
```
 
Obs.: Este Dockerfile é somente de exemplo, não possui os arquivos necessário para fazer o build do programa.

<br>

O Dockerfile Multistage reduziu o tamanho da image para cerca de 10% do tamanho original
```shell
docker image ls                  
REPOSITORY   TAG       IMAGE ID       CREATED          SIZE
go-teste     2.0       7f67163f8905   3 minutes ago    9.56MB
go-teste     1.0       880332e02c30   13 minutes ago   967MB
```
Imagem com a tag 2.0 está usando o Multistage.