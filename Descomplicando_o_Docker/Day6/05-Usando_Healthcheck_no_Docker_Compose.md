# Usando Healthcheck no Docker Compose

<br>

O atributo `healthcheck` declara uma verificação que é executada para determinar se os contêineres de serviço estão ou não "íntegros". Funciona da mesma maneira e tem os mesmos valores padrão da instrução `HEALTHCHECK` do arquivo **Dockerfile**. O Docker Compose pode substituir os valores definidos no Dockerfile.


```docker
services:
  nginx:
    image: nginx:alpine3.20
    ports:
      - "8080:80/tcp"
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost || exit 1"]
      interval: 1m30s
      timeout: 5s
      retries: 3
      start_period: 30s
```
- `test`: Define o comando que o Docker Compose executa para verificar a integridade do container. 
- `interval`: Intervalo de tempo entre os testes.
- `timeout`: Se um único teste demorar mais do que o tempo de *timeout*, o teste será considerado como tendo falhado.
- `retries`: Quantidades consecutivas de falhas para que o container seja considerado `unhealthy`.
- `start_period`: Fornece o tempo de inicialização para containers que precisam de tempo para inicializar.
- `start_interval`: É o tempo entre verificações de integridade durante o período de início. 

**Obs**.: As unidades suportadas são us (microssegundos), ms (milissegundos), s (segundos), m (minutos) e h (horas). 
