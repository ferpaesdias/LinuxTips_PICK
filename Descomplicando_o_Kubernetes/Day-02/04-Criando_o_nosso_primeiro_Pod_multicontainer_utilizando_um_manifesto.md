# Criando o nosso primeiro Pod multi-container utilizando um manifesto[^1]

Ao criar um objeto no Kubernetes, você deve fornecer a especificação do objeto que descreve seu estado desejado, bem como algumas informações básicas sobre o objeto (como um nome).

Quando você usa a API Kubernetes para criar o objeto (diretamente ou via kubectl), essa solicitação de API deve incluir essas informações como JSON no corpo da solicitação.

Na maioria das vezes, você fornece as informações ao kubectl em um arquivo conhecido como **manifesto**. Por convenção, os manifestos são YAML (você também pode usar o formato JSON).

<br>

### Campos obrigatórios

No **manifesto** (arquivo YAML ou JSON) do objeto Kubernetes que você deseja criar, você precisará definir valores para os seguintes campos:

- **apiVersion**: Qual versão da API Kubernetes você está usando para criar este objeto
- **kind**: Que tipo de objeto você deseja criar
- **metadados**: Dados que ajudam a identificar exclusivamente o objeto, incluindo uma string `name`, `UID` e a, opcional, `namespace` 
- **spec**: Qual estado você deseja para o objeto

<br>

## Arquivo YAML

Criar um arquivo YAML para a criação de um Pod usando as flags `--dry-run=client` e `-o yaml`. A saída do comando será redirecionada para o arquivo `pod-exemplo.yaml`:

```shell
kubectl run pod-exemplo --image alpine --dry-run=client -o yaml > pod-exemplo.yaml
```

<br>

Arquivo `pod-exemplo.yaml` gerado com o comando acima:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: pod-exemplo
  name: pod-exemplo
spec:
  containers:
  - image: alpine
    name: pod-exemplo
    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```
<br>

### Adicionando mais campos no arquivo YAML

<br>

Adicionando o `labels` `service` dentro do campo `metadata`:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: pod-exemplo
    service: webserver
  name: pod-exemplo
spec:
  containers:
  - image: nginx
    name: nginx
    resources: {}
  - image: busybox
    name: busybox
    args:
    - sleep
    - "600"
  dnsPolicy: ClusterFirst
  restartPolicy: Always
```

<br>

## Criar um recurso do Kubernetes usando um arquivo YAML

Pode ser utilizados dois comandos para criar um recurso do Kubernetes usando um *manifesto*: `kubectl create` e `kubectl apply`.

O `kubectl create` irá criar os recursos descritos no manifesto, se algum recurso já existir será exibida uma mensagem de erro. 

O `kubectl apply` irá criar os recursos descritos no manifesto, porém, se algum recurso já existir ele será atualizado com as novas configurações.

<br>

### kubectl create[^2]

O `kubectl create` cria um recurso a partir de um arquivo ou stdin.

<br>

Criando um Pod da partir de um arquivo YAML ou JSON:

```shell
kubectl create -f pod-exemplo.yaml
```

<br>

Criando um Pod da partir de um stdin:

```shell
cat pod-exemplo.yaml | kubectl create -f -
```

<br>

### kubectl apply[^3]

O `kubectl apply` aplica a configuração de um recurso a partir de um arquivo ou stdin. Este recurso será criado se não existir.

<br>

Aplicando ou criando as configurações de um Pod da partir de um arquivo YAML ou JSON:

```shell
kubectl apply -f pod-exemplo.yaml
```

<br>

Aplicando ou criando as configurações de um Pod da partir de um stdin:

```shell
cat pod-exemplo.yaml | kubectl apply -f -
```

<br>

## Verificar logs dos Pods[^4]

Mostra os logs de um container em um Pod ou recurso especificado. Se o Pod tiver apenas um container, o nome do container será opcional.

```shell
kubectl logs -f -c nome_container pod-exemplo
```

<br>

## Fontes
[^1]: [Kubernetes: Describing a Kubernetes object](https://kubernetes.io/docs/concepts/overview/working-with-objects/#describing-a-kubernetes-object)
[^2]: [Kubernetes: kubectl-commands create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)
[^3]: [Kubernetes: kubectl-commands apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)
[^4]: [Kubernetes: kubectl-commands logs](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#logs)