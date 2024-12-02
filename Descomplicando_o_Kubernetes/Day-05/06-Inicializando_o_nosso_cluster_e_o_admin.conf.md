# Inicializando o nosso cluster e o admin.conf

<br>


Comandos para inicializar nosso cluster

```shell
# Inicializar o Node Control Plane
sudo kubeadm init --pod-network-cidr=10.10.0.0/16 --apiserver-advertise-address=<IP_Control_Plane>


# Para começar a usar seu cluster, você precisa executar o seguinte como usuário regular (não root)
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config

# Alternativamente, se você for o usuário root, você pode executar
export KUBECONFIG=/etc/kubernetes/admin.conf
```
<br>

### Inicializando o Node Control Plane

Para configurar o endereço de anúncio do API Server para Nodes Control Plane criados com `init` e `join`, a flag `--apiserver-advertise-address` pode ser usada.

<br>

### Começar a usar o seu cluster

O `kubeadm init` primeiro executa uma série de pré-verificações para garantir que a máquina esteja pronta para executar o Kubernetes.

Essas pré-verificações expõem avisos e saem em caso de erros. O `kubeadm init` faz download e instala os componentes do cluster Control Plane. Isso pode levar vários minutos. Depois que terminar você deverá ver instruções de como começar a usar o cluster.

>[!Warning]
**Não compartilhe o arquivo `admin.conf` com ninguém**.  
O arquivo kubeconfig `admin.conf` que o `kubeadm init` gera contém um certificado com `Subject: O = kubeadm:cluster-admins, CN = kubernetes-admin`. O grupo `kubeadm:cluster-admins` está vinculado ao built-in ClusterRole `cluster-admin`.   


>[!Warning]
`kubeadm init` gera outro arquivo kubeconfig `super-admin.conf` que contém um certificado com `Subject: O = system:masters, CN = kubernetes-super-admin`. O item `system:masters` é um grupo de superusuários que ignora a camada de autorização (por exemplo, RBAC).   
**Não compartilhe o arquivo `super-admin.conf` com ninguém. Recomenda-se mover o arquivo para um local seguro.**

<br>

## Organizando o acesso ao cluster usando arquivos kubeconfig

Use arquivos *kubeconfig* para organizar informações sobre clusters, usuários, namespaces e mecanismos de autenticação.

A ferramenta de linha de comando `kubectl` usa arquivos *kubeconfig* para encontrar as informações necessárias para escolher um cluster e se comunicar com o API Server de um cluster.

<br>

>[!Note]
Um arquivo usado para configurar o acesso aos clusters é chamado de arquivo *kubeconfig*. Esta é uma forma genérica de se referir aos arquivos de configuração. Isso não significa que exista um arquivo chamado **kubeconfig**.

<br>

Por padrão, o `kubectl` procura um arquivo chamado config no diretório `$HOME/.kube`. Você pode especificar outros arquivos kubeconfig definindo a variável de ambiente `KUBECONFIG` ou definindo a flag `--kubeconfig`.

<br>

## Arquivo kubeconfig admin.conf

- É um arquivo de configuração do *kubectl*, que é o cliente de linha de comando do Kubernetes. Ele é usado para se comunicar com o cluster Kubernetes.

- Contém as informações de acesso ao cluster, como o endereço do servidor API, o certificado de cliente e o token de autenticação.

- Eu posso ter mais de um contexto dentro do arquivo `admin.conf`, onde cada contexto é um cluster Kubernetes. Por exemplo, eu posso ter um contexto para o cluster de produção e outro para o cluster de desenvolvimento, etc.

- Ele contém os dados de acesso ao cluster, portanto, se alguém tiver acesso a esse arquivo, ele terá acesso ao cluster. (Desde que tenha acesso ao cluster, claro).

- O arquivo `admin.conf` é criado quando o cluster é inicializado.

<br>

## Saiba mais
[Kubernetes: Creating a cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)    
[Kubernetes: Organizing Cluster Access Using kubeconfig Files](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/)    
[Kubernetes: Configure Access to Multiple Clusters](https://kubernetes.io/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)    