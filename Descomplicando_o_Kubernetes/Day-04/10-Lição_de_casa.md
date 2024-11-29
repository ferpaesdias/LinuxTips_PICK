# Lição de casa

<br>

Criar 03 manifestos de Deployment com os seguintes itens: 

- Limite de recursos
- Strategy
- Probes 

<br>

## Primeiro deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: apache-licao01
    licao: "ZeroUm"
  name: apache-licao01
spec:
  replicas: 10
  selector:
    matchLabels:
      app: apache-licao01
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
  template:
    metadata:
      labels:
        app: apache-licao01
    spec:
      containers:
      - image: httpd:2.4.62-alpine3.20
        name: apache
        resources:
          limits:
            cpu: 0.6
            memory: 128Mi
          requests:
            cpu: 0.2
            memory: 64Mi
        livenessProbe:
          exec:
            command:
            - cat
            - /usr/local/apache2/htdocs/index.html
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          httpGet:
            path: /index.html
            port: 80
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        startupProbe:
          tcpSocket:
            port: 80
          initialDelaySeconds: 10
          timeoutSeconds: 5
```

<br>

## Segundo deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: mysql-licao02
    licao: "ZeroDois"
  name: mysql-licao02
spec:
  replicas: 6
  selector:
    matchLabels:
      app: mysql-licao02
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 10%
      maxUnavailable: 25%
  template:
    metadata:
      labels:
        app: mysql-licao02
    spec:
      containers:
      - image: mysql:9.1.0
        name: mysql
        env:
        - name: MYSQL_RANDOM_ROOT_PASSWORD
          value: "yes"
        resources:
          limits:
            cpu: 0.6
            memory: 512Mi
          requests:
            cpu: 0.3
            memory: 256Mi
        livenessProbe:
          exec:
            command:
            - ls
            - /var/lib/mysql/mysql.sock
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          tcpSocket:
            port: 3306
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        startupProbe:
          tcpSocket:
            port: 3306
          initialDelaySeconds: 10
          timeoutSeconds: 5

```

<br>

## Terceiro deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: grafana-licao03
    licao: "ZeroTres"
  name: grafana-licao03
spec:
  replicas: 8
  selector:
    matchLabels:
      app: grafana-licao03
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: grafana-licao03
    spec:
      containers:
      - image: grafana/grafana-oss
        name: grafana
        resources:
          limits:
            cpu: 0.6
            memory: 512Mi
          requests:
            cpu: 0.3
            memory: 256Mi
        livenessProbe:
          exec:
            command:
            - ls
            - /usr/share/grafana/bin/grafana
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          tcpSocket:
            port: 3000
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        startupProbe:
          tcpSocket:
            port: 3000
          initialDelaySeconds: 10
          timeoutSeconds: 5
```