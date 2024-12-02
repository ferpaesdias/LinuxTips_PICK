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

## Seções de um arquivo kubeconfig

<br>

### Clusters

**Clusters** é um mapa de nomes referenciáveis ​​para configurações de cluster.

Cada cluster contém informações sobre como se comunicar com um cluster Kubernetes. Contém o endereço do API server e o certificado de autoridade (`certificate-authority-data`).

- `certificate-authority-data`: O **CertificateAuthorityData** (CA) contém certificados de autoridade de certificação codificados em PEM. O CA é responsável por assinar e emitir certificados para o cluster. O certificado CA é usado para verificar a autenticidade dos certificados apresentados pelo servidor de API e pelos clientes, garantindo que a comunicação entre eles seja segura e confiável.

<br>

Exemplo:

```yaml
clusters:
- cluster:
    certificate-authority-data: <CERTIFICADO>
    server: https://192.168.3.183:6443
  name: kubernetes
```

<br>

### Contexts

**Contexts** é um mapa de nomes referenciáveis ​​para configurações de contexto.

Contexto é uma tupla de referências a um cluster (como me comunico com um cluster kubernetes), um usuário (como me identifico) e um namespace (com qual subconjunto de recursos desejo trabalhar).

Exemplo:

```yaml
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
```

<br>

### Preferences

A seção **preferences** contém configurações globais que afetam o comportamento do *kubectl*. Aqui podemos definir o editor de texto padrão, por exemplo.

<br>

### Users

**Users** contém informações que descrevem informações de identidade. Isso é usado para informar ao cluster Kubernetes quem você é.

Está secão contém as credenciais de acesso dos usuários, como:

- `client-certificate-data`: O **ClientCertificateData** contém dados codificados em PEM de um arquivo de certificado de cliente para TLS. O **ClientCertificateData** é usado para autenticar o usuário ao se comunicar com o API server do Kubernetes. O certificado é assinado pela autoridade de certificação (CA) do cluster e inclui informações sobre o usuário e sua chave pública.

- `client-key-data`: O **ClientKeyData** contém dados codificados em PEM de um arquivo de chave de cliente para TLS. Substitui *ClientKey*. O **ClientKeyData** é usado para assinar as solicitações enviadas ao API server do Kubernetes, permitindo que o servidor verifique a autenticidade da solicitação. A chave privada deve ser mantida em sigilo e não compartilhada com outras pessoas ou sistemas.

- `token`: É um token de acesso que é usado para autenticar o usuário que está executando o comando *kubectl*. Esse token é gerado automaticamente quando o cluster é inicializado.

<br>

Exemplo:

```yaml
contexts:
- context:
    cluster: kubernetes
    user: kubernetes-admin
  name: kubernetes-admin@kubernetes
```

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
[Kubernetes: Reference - kubeconfig (v1)](https://kubernetes.io/docs/reference/config-api/kubeconfig.v1/)    