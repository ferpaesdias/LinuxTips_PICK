# Conhecendo o kubectl attach e o kubectl exec

<br>

## Kubectl run

Executar um Pod de nome `pod-exemplo`

```shell
kubectl run pod-exemplo --image nginx --port 80
```

<br>

Executar um Pod e mantê-lo em primeiro plano, não o reinicie se ele sair

```shell
kubectl run -ti pod-exemplo --image nginx --port 80
```

<br>

## kubectl attach

Anexe a um processo que já está em execução dentro de um container existente.

```shell
kubectl attach pod-exemplo -c nome_container -ti
```

<br>

## kubectl exec

Execute um comando em um container.

<br>

Executando o comando `bash` dentro do container `nome_container` que está no Pod `pod-exemplo`

```shell
kubectl exec -ti pod-exemplo -c nome_container -- bash
```

<br>

## Saiba mais
[Kubernetes: kubectl-commands run](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#run)   
[Kubernetes: kubectl-commands attach](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#attach)   
[Kubernetes: kubectl-commands exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)   