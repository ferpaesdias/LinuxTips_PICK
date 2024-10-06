# Definindo volume no Dockerfile

<br>

- `VOLUME`: Criar persistência de dados.

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

VOLUME /app/dados
CMD ["/app/hello"]
```
