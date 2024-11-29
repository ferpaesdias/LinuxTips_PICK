# Startup probe

<br>

A **startup probe** verifica se o aplicativo em um container foi iniciado. Isso pode ser usado para adotar *liveness probe* em containers de inicialização lenta, evitando que sejam encerrados pelo *kubelet* antes de estarem em funcionamento.

Se a **startup probe** estiver configurada, ela desabilitará as *liveness probe* e *readiness probe* até que seja bem-sucedida.

A **startup probe** é executado apenas na inicialização, diferentemente das *liveness probe* e *readiness probe*, que são executados periodicamente.

<br>

A **startup probe** têm vários campos que você pode usar para controlar com mais precisão o comportamento das verificações de inicialização, atividade e prontidão:

- `initialDelaySecond`: Informa ao *kubelet* o tempo em segundos que ele deve esperar antes de executar a primeira investigação. O valor padrão é `0` e o valor mínimo é `0`.

- `periodSeconds`: Informa ao *kubelet* a frequência em segundos que será realizada a verificação. O valor padrão é `10` e o valor mínimo é `1`.

- `timeoutSeconds`: O número de segundos que será considerado como falha após uma verificação falhar.  O valor padrão é `1` e o valor mínimo é `1`.

- `successThreshold`: A quantidade mínima de "success"  consecutivas após uma falha para a verificação ser considerada bem-sucedida.  O valor padrão é `1`. Deve ser `1`para *liveness probe* e *startup probe* e o valor mínimo é `1`.

- `failureThreshold`: A quantidade falhas consecutivas para a verificação ser considerada "failure". O Kubernetes considera que a verificação geral falhou: o container não está ready/healthy/live. O valor padrão é `3` e o valor mínimo é `1`. Para o caso de *liveness probe* ou *startup probe*, se pelo menos as sondagens de failThreshold falharem, o Kubernetes tratará o container como não íntegro e acionará uma reinicialização para esse container específico. Para uma *readiness probe* com falha, o *kubelet* continua executando o container que falhou nas verificações e também continua a executar mais análises; como a verificação falhou, o *kubelet* define a condição `Ready` no Pod como `falsa`.
`
- `terminationGracePeriodSeconds`: Define um período de carência, em segundos, para o *kubelet* aguardar entre o acionamento do desligamento do container com falha e, em seguida, forçar o *container runtime* a interrompê-lo. O valor padrão é `30` e o valor mínimo é `1`. 

<br>

A **readiness probe** e a **liveness probe** não dependem uma da outra para serem bem-sucedidas. Se quiser esperar antes de executar uma **readiness probe**, você deve usar `InitialDelaySeconds` ou **startup probe**.

A **readiness probe** e a **liveness probe** podem ser usadas em paralelo para o mesmo container. O uso de ambos pode garantir que o tráfego não chegue a um container que não esteja pronto para isso e que os containers sejam reiniciados quando falharem.

<br>

## TCP startup probe

Com esta configuração, o *kubelet* tentará abrir um soquete para o seu container na porta especificada. Se conseguir estabelecer uma conexão, o container é considerado íntegro; caso contrário, é considerado uma falha.

Exemplo de um manifesto com **TCP startup probe**

<br>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  strategy: {}
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
      - image: nginx
        name: nginx
        resources:
          limits:
            cpu: 0.5
            memory: 256Mi
          requests:
            cpu: 0.3
            memory: 64Mi
        livenessProbe:
          tcpSocket:
            port: 80
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          tcpSocket:
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

## startup HTTP request

O *kubelet* envia uma solicitação HTTP GET para o servidor que está em execução no container e escutando na porta 80 (`port: 80`).

Se caminho, descrito no campo `path:`, do servidor retornar um código de sucesso, o *kubelet* considerará o container ativo e saudável. Se o manipulador retornar um código de falha, o *kubelet* encerra o container e o reinicia.

Exemplo de um manifesto com **startup HTTP request**

<br>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  strategy: {}
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
      - image: nginx
        name: nginx
        resources:
          limits:
            cpu: 0.5
            memory: 256Mi
          requests:
            cpu: 0.3
            memory: 64Mi
        livenessProbe:
          httpGet:
            path: /index.html
            port: 80
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
          periodSeconds: 10
```

<br>

## startup command

Para realizar uma verificação, o *kubelet* executa o comando `cat /usr/share/nginx/html/index.html`, configurado no campo `command`, no container de destino.

Se o comando for bem-sucedido, ele retornará `0` e o *kubelet* considerará o container ativo e íntegro. Se o comando retornar um valor diferente de zero, o *kubelet* encerra o container e o reinicia.

Exemplo de um manifesto com **startup command**

<br>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  strategy: {}
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
      - image: nginx
        name: nginx
        resources:
          limits:
            cpu: 0.5
            memory: 256Mi
          requests:
            cpu: 0.3
            memory: 64Mi
        livenessProbe:
          exec:
            command:
            - cat
            - /usr/share/nginx/html/index.html
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        readinessProbe:
          exec:
            command:
            - cat
            - /usr/share/nginx/html/index.html
          initialDelaySeconds: 10
          periodSeconds: 10
          timeoutSeconds: 5
          failureThreshold: 3
        startupProbe:
          tcpSocket:
            port: 80
          initialDelaySeconds: 10
          periodSeconds: 10
```

<br>

## Saiba mais
[Kubernetes: Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)