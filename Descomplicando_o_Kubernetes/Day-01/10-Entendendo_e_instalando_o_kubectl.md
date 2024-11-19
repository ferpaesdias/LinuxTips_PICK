# Entendendo e instalando o kubectl

<br>

## Instalação do kubectl no Linux[^1]

Instalação do `kubectl` no Linux (x86-64) usando o `curl`:

```shell
   curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
   sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl
```

<br>

Para testar a instalação 

```shell
kubectl version --client
```

<br>

## Fontes
[^1]: [Kubernetes: Install and Set Up kubectl on Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)