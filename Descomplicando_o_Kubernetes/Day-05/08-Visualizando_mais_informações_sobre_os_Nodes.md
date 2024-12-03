# Visualizando mais informações sobre os Nodes

<br>

### 

Mostra uma tabela com as informações sobre os Nodes 

```shell
kubectl get nodes
```

<br>

Mostra uma tabela com as informações mais importantes sobre os Nodes, como *IP*, a *versão do Kernel*, o *container runtime*, etc

```shell
kubectl get nodes -o wide
```

<br>

Mostra uma descrição detalhada dos Nodes, incluindo recursos relacionados, como eventos ou controladores.  

```shell
kubectl describe nodes
```

<br>

Mostra uma descrição detalhada de determinado Node, incluindo recursos relacionados, como eventos ou controladores. 

```shell
kubectl describe nodes <NOME_NODE>
```

<br>

Mostra uma descrição detalhada de determinado Node no formato YAML
```shell
kubectl describe nodes <NOME_NODE> -o yaml
```

<br>

## Saiba mais
[Kubernetes: Kubectl Commands](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)