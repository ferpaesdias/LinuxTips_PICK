# Conhecendo o YAML e kubectl com dry-run

<br>


Você pode usar a flag `--dry-run=client` para visualizar o objeto que seria enviado ao seu cluster, sem realmente enviá-lo.

```shell
kubectl run --image nginx --port 80 pod-exemplo --dry-run=client
```

<br>

A flag `--dry-run=client` junto com a flag `-o yaml` pode ser usada para criar um arquivo `.yaml` com os parâmetros do objeto


```shell
kubectl run --image nginx --port 80 pod-exemplo --dry-run=client -o yaml > pod-exemplo.yaml
```

<br>

Cria um Pod usando o arquivo YAML criado no exemplo anterior

```shell
kubectl apply -f pod.yaml
```