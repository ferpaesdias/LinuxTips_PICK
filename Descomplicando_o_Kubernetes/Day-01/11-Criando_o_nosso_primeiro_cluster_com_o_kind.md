# Criando o nosso primeiro cluster com o kind

<br>

## Instalação do kind no Linux

Instalação do `kind' no Linux (x86-64):

```shell
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.25.0/kind-linux-amd64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

<br>

Testar a instalação:

```shell
kind version
```

<br>

## Criar um cluster


Criar um cluster 

```shell
kind create cluster
```

<br>

## Criar clusters a partir de um arquivo

Criar um cluster cluster com 01 Node Control Plane e 02 Nodes Workers a partir de um arquivo `.yaml`.

Arquivo `kind-cluster.yaml`:

```yaml
kind: Cluster
apiVersion: kind.x-k8s.io/v1alpha4
nodes:
- role: control-plane
- role: worker
- role: worker
```
<br>

Comando para criar o cluster:

```shell
kind create cluster --config kind-cluster.yaml --name kind-exemplo
```

<br>

## Listar clusters

Listar clusters

```shell
kind get clusters
```

<br>

## Remover um cluster

Remover um cluster 

```shell
kind delete cluster
```

<br>

## Saiba mais
[Kind: Quick Start](https://kind.sigs.k8s.io/docs/user/quick-start/)