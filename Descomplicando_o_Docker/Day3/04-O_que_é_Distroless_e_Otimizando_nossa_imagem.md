# O que é Distroless e otimizando nossa imagem 

<br>

As imagens "Distroless" contêm apenas seu aplicativo e suas dependências de tempo de execução. Eles não contêm gerenciadores de pacotes, shells ou quaisquer outros programas que você esperaria encontrar em uma distribuição Linux padrão.

<br>

## Images Directory

[Chainguard](https://images.chainguard.dev/?_gl=1*jotfr4*_gcl_au*MTQyMjIwMjExNi4xNzI4MzI2MDYz)

[Google](https://github.com/GoogleContainerTools/distroless?tab=readme-ov-file#how-do-i-use-distroless-images)

<br>

## Construindo o App com o Chainguard

```dockerfile
FROM cgr.dev/chainguard/python:latest-dev AS builder
WORKDIR /app
RUN python -m venv venv
ENV PATH="/app/venv/bin":$PATH
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

FROM cgr.dev/chainguard/python:latest
WORKDIR /app
COPY app.py .
COPY --from=builder /app/venv /app/venv
ENV PATH="/app/venv/bin:$PATH"
COPY static static/
COPY templates templates/
EXPOSE 5000
ENV REDIS_HOST=<IP_DO_HOST>
ENTRYPOINT ["python", "-m", "flask", "run", "--host=0.0.0.0"]

```

Obs.: Arquivo somente para consulta, não possui as dependências necessárias.

<br>

---
## Saiba mais
["Distroless" Container Images](https://github.com/GoogleContainerTools/distroless)