# Recomendações para criar um cluster Kubernetes

<br>


Recomendações para criar um cluster Kubernetes:

- Uma máquina com sistema operacional Linux compatível. O projeto Kubernetes provê instruções para distribuições Linux baseadas em Debian e Red Hat, bem como para distribuições sem um gerenciador de pacotes.

- 02 GB ou mais de RAM por máquina (menos deixará pouco espaço para seus aplicativos).

- 02 CPUs ou mais

- Conexão de rede entre todas as máquinas no cluster. Seja essa pública ou privada.

- Nome de host único, endereço MAC e product_uuid para cada nó. Veja [aqui](https://kubernetes.io/pt-br/docs/setup/production-environment/tools/kubeadm/install-kubeadm/#verify-mac-address) para mais detalhes.

- As seguintes portas devem estar abertas em suas máquinas (todas TCP): 2379-2380, 6443, 10250-10257, 10259, 30000-32767, etc. Veja [aqui](https://kubernetes.io/docs/reference/networking/ports-and-protocols/) para mais detalhes.

- Configuração de swap. O comportamento padrão do kubelet era falhar ao iniciar se a memória swap fosse detectada em um Node. O suporte a swap foi introduzido a partir da v1.22. E desde a v1.28, o swap é suportado apenas para cgroup v2; o recurso NodeSwap do kubelet está em beta, mas desativado por padrão.
    - Você DEVE desabilitar o swap se o kubelet não estiver configurado corretamente para usar swap. Por exemplo, sudo `swapoff -a` desabilitará a troca temporariamente. Para tornar essa mudança persistente entre reinicializações, certifique-se de que o swap esteja desabilitado em arquivos de configuração como `/etc/fstab`, `systemd.swap`, dependendo de como foi configurado em seu sistema.

<br>

## Saiba mais
[Kubernetes: Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)
