# Docker Compose review avançado

<br>

Docker Compose com mais atributos:

```docker
services:
  name_service01:
    build: 
      context: ./caminho_contexto
      dockerfile: Dockerfile
    container_name: nome_container
    ports:
      - "8080:80"
    environment:
      - VAR: valor
    env_file:
      - .env
    volumes:
      - type: volume
        source: name_volume
        target: /caminho/volume
    networks:
      - name_network
    deploy:
      labels:
        com.domain.descriptions: "Descrição do container"
        com.domain.version: "Versão do container"
      resources:
        reservations:
          cpus: '0.25'
          memory: 128M
        limits:
          cpus: '0.5'
          memory: 256M
      restart_policy:
        condition: on-failure
        delay: 5s
        max_attempts: 3
    dns:
      - 8.8.8.8
      - 8.8.4.4
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost || exit 1"]
      interval: 1m30s
      timeout: 5s
      retries: 3
      start_period: 30s

  name_service02:
    build: ./caminho_Dockerfile
      context: ./caminho_contexto
    command: insira um comando
    deploy:
      replicas: 4
      update_config:
        parallelism: 2
        delay: 10s
      resources:
        reservations:
          cpus: '0.25'
          memory: 128M
        limits:
          cpus: '0.5'
          memory: 256M    
    depends_on:
      - nome_service01
    devices:
      - "/dev/ttyUSB0:/dev/ttyUSB0"

volumes:
  name_volume:
    name: "name_volume"
    
networks:
  name_network:
    name: "name_network"
    driver: bridge
    ipam:
      driver: default
      config:
        - subnet: "192.168.20.0/24"

```
