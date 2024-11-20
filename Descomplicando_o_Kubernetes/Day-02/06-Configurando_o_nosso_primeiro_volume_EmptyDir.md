# Configurando o nosso primeiro volume EmptyDir[^1]

Como o nome diz, o volume **emptyDir** está inicialmente vazio. Todos os containers no Pod podem ler e gravar os mesmos arquivos no volume **emptyDir**, embora esse volume possa ser montado no mesmo caminho ou em caminhos diferentes em cada container.

Quando um Pod é removido de um Node por qualquer motivo, os dados em **emptyDir** são excluídos permanentemente.

<br>

>[!Note]
A falha de um container não remove um Pod de um Node. Os dados em um volume **emptyDir** estão seguros em caso de falhas no container.

<br>

## Exemplo

Neste exemplo, foi definido um volume do tipo **emptyDir**, com o tamanho de 256MB e de nome *primeiro-emptydir*:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: pod-exemplo
  name: pod-exemplo
spec:
  containers:
  - image: nginx
    name: webserver
    volumeMounts:
    - mountPath: /webserver
      name: primeiro-emptydir
    resources:
      limits:
        cpu: "1"
        memory: "128Mi"
      requests:
        cpu: "0.5"
        memory: "64Mi"

  dnsPolicy: ClusterFirst
  restartPolicy: Always
  volumes:
  - name: primeiro-emptydir
    emptyDir:
      sizeLimit: 256Mi
  ```

<br>

## Fontes
[^1]: [Kubernetes: Volumes emptyDir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir)