# Primeiros passos no Kubernetes com o kubectl

Kubernetes fornece uma ferramenta de linha de comando para comunicação com o **Control Plane** de um cluster Kubernetes, usando a API Kubernetes.

Esta ferramenta é chamada **kubectl**.

Para configuração, **kubectl** procura um arquivo chamado `config` no diretório `$HOME/.kube`. Você pode especificar outros arquivos kubeconfig definindo a variável de ambiente `KUBECONFIG` ou definindo a flag `--kubeconfig`.

<br>

## Syntax

O comando `kubectl` utiliza a seguinte sintaxe:

```shell
kubectl [command] [TYPE] [NAME] [flags]
```
- `command`: Especifica a operação que você quer executar em um ou mais recursos, por exemplo `create`, `get`, `describe`, `delete`.

- `TYPE`: Especifica o *Resource Type*. O *Resource Type* é case-insensitive e você pode especificar no singular, plural ou de forma abreviada. Por exemplo, os seguintes comando produzem a mesma saída: `kubectl get pod pod1`, `kubectl get pods pod1`, `kubectl get po pod1`.

- `NAME`: Especifica o nome do recurso. O **NAME** é case-sensitive. Se o **NAME** é omitido, os detalhes de todos os recursos são mostrados, por exemplo, `kubectl get pods`.

- `flags`: Especifica flags opcionais. Por exemplo, você pode usar `-s` ou `--server` para especificar o endereço e porta do Kubernetes API Server.

<br>

## Exemplos do comando kubectl

Listar Pods 

```shell
kubectl get pods
```

<br>

Listar Deployments do **namespace** `kube-system`

```shell
kubectl get deployment -n kube-system
```

<br>

Listar ReplicaSets do **namespace** `kube-system` e com mais informações usando o parâmetro `-o wide`

```shell
kubectl get replicaset -n kube-system -o wide
```

<br>

Listar todos os Services independentemente do *namespace*

```shell
kubectl get service -A
```

<br>


Crie e execute uma imagem específica em um Pod com o nome *pod-exemplo*

```shell
kubectl run --image nginx --port 80 pod-exemplo
```

<br>

Acessar um Pod, que possui somente um container, que está em execução

```shell
kubectl exec -ti pod-exemplo -- bash
```

<br>

Deletar um Pod

```shell
kubectl delete pod pod-exemplo 
```

<br>

## Saiba mais
[Kubernetes: Command line tool (kubectl)](https://kubernetes.io/docs/reference/kubectl/)