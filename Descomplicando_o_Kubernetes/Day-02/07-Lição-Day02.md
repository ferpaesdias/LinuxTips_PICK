# Lição Day02

<br>

Criar um manifesto de um Pod com o maior número de campos

```yaml
metadata:
  name: nginx
  namespace: licao-day02
  labels:
    environment: production
    app: licaoDay02
    licao: Day02
spec:
  containers:
  - name: nginx
    image: nginx:1.17.0
    env:
    - name: VAR1
      value: "valor1"
    ports:
    - containerPort: 80
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
    volumeMounts:
    - mountPath: /app
      name: debian-app
      readOnly: false
    args:
    command: ["sleep"]
    args: ["600"]
  restartPolicy: Always
```

Manifesto em constante atualização. 