# Adicionando outros Nodes e o que é CNI

<br>

## Adicionando outros Nodes

O comando `kubeadm join` inicializa um novo Node Kubernetes e o une ao cluster existente.

O `kubeadm join` foi exibido na saída do `kubeadm init`. Por exemplo:

```shell
kubeadm join 172.20.0.10:6443 --token abcd123.bhiyqbaqldu47894 --discovery-token-ca-cert-hash sha256:aaa359d6da9bd5f8f0155d33b3c000a78386ee052b17f044c6dcc37be02ffzzz
```
- `172.20.0.10:6443`: Endereço IP e porta do Node Control Plane. Neste exemplo, o nosso Node Control Plane possui o IP `172.20.0.10` e a porta `6443`.
- `--token`:  Os tokens são usados ​​para estabelecer confiança bidirecional entre um Node que ingressa no cluster e um Node Control Plane.
- `--discovery-token-ca-cert-hash`: Valida a chave pública da autoridade de certificação (CA) raiz apresentada pelo Control Plane do Kubernetes. O valor deste sinalizador é especificado como `<hash-type>:<hex-encoded-value>`, onde o tipo de hash suportado é "sha256". O hash é calculado sobre os bytes do objeto Subject Public Key Info (SPKI) (como em RFC7469).

<br>

Os tokens expiram em 24h. Se o token estiver expirado, ou não copiou a saída do comando `kubeadm init`, use o comando abaixo para gerar um novo token e mostrar o comando `kubeadm join` que deve ser executado para inicializar um novo node:

```shell
kubeadm token create --print-join-command
```

<br>

## CNI - Container Network Interface

**CNI** (Container Network Interface), um projeto Cloud Native Computing Foundation, consiste em uma especificação e bibliotecas para escrever plug-ins para configurar interfaces de rede em containers Linux, junto com vários plug-ins suportados.

A **CNI** se preocupa apenas com a conectividade de rede dos containers e com a remoção de recursos alocados quando o container é excluído. 

Com isso, temos diferentes plugins de redes, que seguem a especificação CNI, e que podem ser utilizados no Kubernetes. O Weave Net é um desses plugins de rede.

<br>

### Plugins

Após unir um Node ao Node Control Plane e executar o comando `kubectl get nodes` no Node Control Plane, o status dos Nodes será `NotReady`.

Isso acontece porque está faltando o plugin de rede para que seja possível a comunicação entre os Pods.

```
NAME                  STATUS      ROLES           AGE   VERSION
debian-kubernetes01   NotReady    control-plane   84m   v1.31.3
debian-kubernetes02   NotReady    <none>          83m   v1.31.3
debian-kubernetes03   NotReady    <none>          83m   v1.31.3
```
<br>

Entre os plugins de rede mais utilizados no Kubernetes, temos:

- **Calico**: é um dos plugins de rede mais populares e amplamente utilizados no Kubernetes. Ele fornece segurança de rede e permite a implementação de políticas de rede. O **Calico** utiliza o BGP (Border Gateway Protocol) para rotear tráfego entre os Nodes do cluster, proporcionando um desempenho eficiente e escalável.

- **Flannel**: é um plugin de rede simples e fácil de configurar, projetado para o Kubernetes. Ele cria uma rede overlay que permite que os Pods se comuniquem entre si, mesmo em diferentes Nodes do cluster. O Flannel atribui um intervalo de IPs a cada Node e utiliza um protocolo simples para rotear o tráfego entre os Nodes.

- **Cilium**: é uma solução de rede, observabilidade e segurança com um plano de dados baseado em eBPF. Ele fornece uma rede simples e plana de Camada 3 com a capacidade de abranger vários clusters em um roteamento nativo ou no modo de sobreposição. Ele reconhece o protocolo L7 e pode impor políticas de rede em L3-L7 usando um modelo de segurança baseado em identidade que é dissociado do endereçamento de rede.

- **Kube-router**:  é uma solução de rede leve para Kubernetes. Ele utiliza o BGP e IPVS (IP Virtual Server) para rotear o tráfego entre os Nodes do cluster, proporcionando um desempenho eficiente e escalável. **Kube-router** também suporta políticas de rede e permite a implementação de firewalls entre os Pods.

- **Weave**: é outra solução popular de rede para Kubernetes. Ele fornece uma rede overlay que permite a comunicação entre os Pods em diferentes Nodes. Além disso, o **Weave** suporta criptografia de rede e gerenciamento de políticas de rede. Ele também pode ser integrado com outras soluções, como o *Calico*, para fornecer recursos adicionais de segurança e políticas de rede.

<br>

O **Weave** é plugin de rede que será demonstrado neste documento. 

Para instalar o plugin **Weave** execute o comando abaixo no Node Control Plane. Como o plugin é um *DaemonSet*, será criado um Pod para cada Node do cluster.

```shell
kubectl apply -f https://github.com/weaveworks/weave/releases/download/v2.8.1/weave-daemonset-k8s.yaml
```

<br>

Após a instalação do plugin **Weave** o status dos Pods passa a ser `Ready`:

```shell
NAME                  STATUS   ROLES           AGE   VERSION
debian-kubernetes01   Ready    control-plane   17h   v1.31.3
debian-kubernetes02   Ready    <none>          17h   v1.31.3
debian-kubernetes03   Ready    <none>          17h   v1.31.3
```

<br>

## Saiba mais
[Kubernetes: kubeadm join](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-join/)    
[Kubernetes: kubeadm token](https://kubernetes.io/docs/reference/setup-tools/kubeadm/kubeadm-token/)  
[Kubernetes: Network Plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)    
[GitHub: Calico](https://github.com/projectcalico/calico)     
[GitHub: Flannel](https://github.com/flannel-io/flannel)   
[GitHub: Cilium](https://github.com/cilium/cilium)   
[GitHub: Weave](https://github.com/weaveworks/weave) 
