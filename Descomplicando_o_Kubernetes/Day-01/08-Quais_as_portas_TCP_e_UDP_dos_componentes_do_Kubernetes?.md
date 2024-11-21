# Quais as portas TCP e UDP dos componentes do Kubernetes?

Quando executamos o Kubernetes em um ambiente com limites de redes rígidos, com datacenters on-premises com firewall de rede ou redes virtuais em nuvens públicas, é útil estar ciente das portas e protocolos usados pelos componentes do Kubernetes.

<br>

### Control Plane

| Protocol | Direction | Port Range | Purpose | Used by |
| :-: | :-: | :-: | :-: | :-: |
| TCP | inbound | 6443 |  Kubernetes API Server | All |
| TCP | inbound | 2379-2380 | etcd server cliente API | kube-apiserver, etcd | 
| TCP | inbound | 10250 | Kubelet API | Self, Control Plane |
| TCP | inbound | 10259 | kube-scheduler | Self |
| TCP | inbound | 10257 | kube-controller-manager | Self |

Embora as portas *etcd* estejam incluídas na seção do *Control Plane*, você também pode hospedar seu próprio cluster *etcd* externamente ou em portas personalizadas.

<br>

### Worker node(s)

| Protocol | Direction | Port Range | Purpose | Used by |
| :-: | :-: | :-: | :-: | :-: |
| TCP | inbound | 10250 |  Kubelet API | Self, Control Plane |
| TCP | inbound | 10256 | kube-proxy | Self, Load balancers | 
| TCP | inbound | 30000-32767 | NodePort Services | All |

<br>

>[!IMPORTANT]
Todas as portas podem ser substituídas. Quando utilizar portas customizadas, essas portas precisam ser abertas ao invés das portas mencionadas acima.

<br>

## Saiba mais
[Kubernetes: Ports and Protocols](https://kubernetes.io/docs/reference/networking/ports-and-protocols/)