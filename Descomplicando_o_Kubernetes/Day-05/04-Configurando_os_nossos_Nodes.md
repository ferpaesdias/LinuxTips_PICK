## Configurando os nossos Nodes

<br>

```shell
# Desativar swap
sudo swapoff -a

# Acessar o arquivo /etc/fstab e comentar a configuração de swap
vim /etc/fstab

# Carregar módulos do Kernel
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
overlay
br_netfilter
EOF

sudo modprobe overlay
sudo modprobe br_netfilter

# Configurar parâmetros do sistema
cat <<EOF | sudo tee /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-iptables  = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.ipv4.ip_forward                 = 1
EOF

sudo sysctl --system

# Instalar kubeadm, kubelet e kubectl (Debian-based)
sudo apt-get update
sudo apt-get install -y apt-transport-https ca-certificates curl gpg

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.31/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.31/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list

sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
sudo apt-mark hold kubelet kubeadm kubectl
```

<br>

## Configuração do Swap

O comportamento padrão de um kubelet é falhar ao iniciar se a memória swap for detectada em um Node. Isso significa que o swap deve ser desabilitada ou tolerada pelo kubelet.

<br>

### Para tolerar o swap

Adicione `failSwapOn: false` à configuração do kubelet ou como argumento de linha de comando.

>[!Note]
Mesmo que `failSwapOn: false` seja fornecido, as cargas de trabalho não teriam acesso de swap por padrão. Isso pode ser alterado definindo um `swapBehavior`, novamente no arquivo de configuração do kubelet. Para usar swap, defina um `swapBehavior` diferente da configuração padrão `NoSwap`. 

<br>

### Para desabilitar o swap

O comando `sudo swapoff -a` pode ser usado para desabilitar o swap temporariamente. Para tornar essa alteração persistente durante as reinicializações, certifique-se de que o swap esteja desabilitada em arquivos de configuração como `/etc/fstab`, `systemd.swap`, dependendo de como foi configurado em seu sistema.

<br>

## Instalando kubeadm, kubelet e kubectl

Você instalará estes pacotes em todas as suas máquinas:

- **kubeadm**: o comando para inicializar o cluster.

- **kubelet**: o componente que é executado em todas as máquinas do seu cluster e faz coisas como iniciar Pods e containers.

- **kubectl**: o utilitário de linha de comando para se comunicar com seu cluster.

<br>

## Saiba mais
[Kubernetes: Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)