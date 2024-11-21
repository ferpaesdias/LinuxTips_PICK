# Os sensacionais kubectl get pods e o kubectl describe pods

<br>

## kubectl get

O `kubectl get` mostra uma tabela com as informações mais importantes sobre os recursos especificados.

Você pode filtrar a lista por label com a flag `--selector`. Se o tipo de recurso desejado tiver namespace, você verá apenas resultados em seu namespace atual, a menos que passe `--all-namespaces` ou `-A`.

Objetos não inicializados não são mostrados a menos que a flag `--include-uninitialized` seja passada.

Ao especificar a saída como 'template' e fornecer um template Go como o valor da flag `--template`, você pode filtrar os atributos dos recursos buscados.

Use `kubectl api-resources` para obter uma lista completa de recursos suportados.

<br>

Comando para listar os Pods

```shell
kubectl get pods
```

<br>

Listar todos os Pods independentemente do *namespace*

```shell
kubectl get pods -A
```

<br>

Listar todos os Pods do *namespace* `kube-system`

```shell
kubectl get pods -n kube-system
```

<br>

Listar Pods do **namespace** `kube-system` e com mais informações usando o parâmetro `-o wide`

```shell
kubectl get pods -n kube-system -o wide
```

<br>

Gerar uma saída YAML do Pod `pod-exemplo`

```shell
kubectl get pods pod-exemplo -o yaml
```

<br>

## kubectl describe

O `kubectl describe` mostra uma descrição detalhada dos recursos selecionados, incluindo recursos relacionados, como eventos ou controladores.

Você pode selecionar um único objeto por nome, todos os objetos desse tipo, fornecer um prefixo de nome ou um label.

<br>

Mostrar os detalhes do Pod `pod-exemplo`

```shell
kubectl describe pods pod-exemplo
```

<br>

## Saiba mais
[Kubernetes: kubectl-commands get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)    
[Kubernetes: kubectl-commands describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)