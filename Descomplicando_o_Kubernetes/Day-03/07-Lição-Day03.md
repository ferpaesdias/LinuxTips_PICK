# Lição Day03

<br>

Criar um manifesto de objeto *Deployment* com o maior número de campos

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-licao-day03
  namespace: licao-day03
  labels:
    environment: production
    app: licaoDay03
    licao: Day03
spec:
  selector:
    matchLabels:
      app: licaoDay03
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
  template:
    metadata:
      labels:
        app: licaoDay03
    spec:
      containers:
        - name: nginx
          image: nginx:1.17.0
          env:
            - name: VAR1
              value: "valor1"
          ports:
            - containerPort: 8080
              name: http
              protocol: TCP
          resources:
            requests:
              cpu: 0.3
              memory: 64Mi
            limits:
              cpu: 0.5
              memory: 128Mi
        - name: debian
          image: debian:11
          command: ["sleep"]
          args: ["600"]
          resources:
            requests:
              cpu: 0.3
              memory: 64Mi
            limits:
              cpu: 0.5
              memory: 128Mi
      restartPolicy: Always
```

Manifesto em constante atualização. 