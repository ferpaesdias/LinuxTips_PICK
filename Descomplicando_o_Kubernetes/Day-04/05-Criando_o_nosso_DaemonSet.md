# Criando o nosso DaemonSet

<br>

Exemplo de um *manifesto* de um **DaemonSet**:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  labels:
    app: node-exporter-daemonset
  name: node-exporter-daemonset
spec:
  selector:
    matchLabels:
      app: node-exporter-daemonset
  template:
    metadata:
      labels:
        app: node-exporter-daemonset
    spec:
      hostNetwork: true
      containers:
        - name: node-exporter
          image: prom/node-exporter:latest
          ports:
          - containerPort: 9100
            hostPort: 9100
          volumeMounts:
          - name: proc
            mountPath: /host/proc
            readOnly: true
          - name: sys
            mountPath: /host/sys
            readOnly: true
      volumes:
      - name: proc
        hostPath:
          path: /proc
      - name: sys
        hostPath:
          path: /sys
```

<br>

### Campos obrigatórios

<br>

Um **DaemonSet** precisa de campos:

- apiVersion
- kind
- metadados

<br>

## Atualizando um DaemonSet

Se os `labels` dos Nodes forem alterados, o **DaemonSet** adicionará imediatamente Pods aos Nodes recém-correspondentes e excluirá Pods dos Nodes recentemente não correspondentes.

Você pode modificar os Pods criados por um **DaemonSet**. No entanto, os Pods não permitem que todos os campos sejam atualizados. Além disso, o controlador **DaemonSet** usará o modelo original na próxima vez que um Node (mesmo com o mesmo nome) for criado.

Você pode excluir um **DaemonSet**. Se você especificar `--cascade=orphan` com `kubectl`, os Pods serão deixados nos Nodes. Se você criar posteriormente um novo **DaemonSet** com o mesmo seletor, o novo **DaemonSet** adotará os Pods existentes. Se algum Pod precisar ser substituído, o **DaemonSet** os substitui de acordo com sua updateStrategy.

Você pode realizar um *rolling update* em um **DaemonSet**.

<br>

## Saiba mais
[Kubernetes: DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)