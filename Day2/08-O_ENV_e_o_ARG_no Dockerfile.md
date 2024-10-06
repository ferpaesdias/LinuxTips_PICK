# O ENV e o ARG no Dockerfile

<br>

- `ENV`: Adiciona uma variável de ambiente à imagem
- `ARG`: Adiciona uma variável que será utilizada somente durante o build da imagem.

```dockerfile
FROM golang:1.18 AS builder
WORKDIR /app
COPY hello.go ./
RUN go mod init hello
RUN go build -o /app/hello

FROM alpine:3.20
COPY --from=builder /app/hello /app/hello
ENV APP="hello"
ARG GIROPOPS="strigus"
ENV GIROPOPS=$GIROPOPS
RUN echo "O giropops é: $GIROPOPS"
CMD ["/app/hello"]
```

<br>

Para alterar valor de um argumento na build da imagem é só adicionar a flag `--build-arg` mais o argumento conforme o exemplo abaixo:

```powershell
docker image build -t go-teste:4.0 --build-arg GIROPOPS=girus .
```
