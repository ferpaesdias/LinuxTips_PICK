# Limitando o consumo de recursos de CPU e Memória[^1]

<br>

Ao especificar um Pod, você pode especificar opcionalmente quanto de cada recurso um container precisa. Os recursos mais comuns a serem especificados são *CPU* e *memória* (RAM).

Quando você especifica os recursos em **request** para os containers em um pod, o *kube-scheduler* usa essas informações para decidir em qual Node colocar o Pod.

Quando você especifica os recursos **limits** para um container, o kubelet impõe esses limites para que o container em execução não tenha permissão para usar mais desses recursos do que o limite definido.

O kubelet também reserva pelo menos a quantidade determinada em **request** desse recurso do sistema especificamente para uso daquele container.

<br>

### Unidades de CPU

**Limits** e **requests** de recursos de CPU são medidos em unidades de CPU. No Kubernetes, 1 unidade de CPU equivale a 1 núcleo de CPU físico ou 1 núcleo virtual, dependendo se o Node é um host físico ou uma máquina virtual rodando dentro de uma máquina física.

Ao definir um container com `0.5` de CPU, você está solicitando metade do tempo de CPU em comparação com se solicitasse `1.0` de CPU. 

Para unidades de recursos de CPU, a expressão quantitativa `0.1` equivale à expressão `100m`, que pode ser lida como “cem milicpu”. Algumas pessoas dizem “cem milicores”, e isso significa a mesma coisa.

O recurso da CPU é sempre especificado como uma quantidade absoluta de recurso, nunca como uma quantidade relativa. Por exemplo, `0.5` de CPU representam aproximadamente a mesma quantidade de poder de computação, quer esse container seja executado em uma máquina de núcleo único, núcleo duplo ou 48 núcleos.

<br>

### Unidades de Memória

**Limits** e **requests** de memória são medidos em *bytes*. Você pode expressar a memória como um número inteiro simples ou como um número de ponto fixo usando um destes sufixos de quantidade: E, P, T, G, M, k. Você também pode usar os equivalentes de potência de dois: Ei, Pi, Ti, Gi, Mi, Ki.

Por exemplo, o seguinte representa aproximadamente o mesmo valor:

```
128974848, 129e6, 129M,  128974848000m, 123Mi
```
<br>

>[!Note]
>Preste atenção nos sufixos. Se você solicitar `400m` de memória, será uma solicitação de 0,4 bytes. Alguém que digitou isso provavelmente pretendia pedir 400 mebibytes (`400Mi`) ou 400 megabytes (`400M`).

<br>

### Exemplo

<br>

No exemplo abaixo foram adicionados os campos `limits` e `resources` no container *ubuntu*:

```yaml
apiVersion: v1
kind: Pod
metadata:
  labels:
    run: pod-exemplo
  name: pod-exemplo
spec:
  containers:
  - image: ubuntu
    name: ubuntu
    args:
    - sleep
    - "1800"
    resources:
      limits:
        cpu: "0.5"
        memory: "128Mi"
      requests:
        cpu: "0.3"
        memory: "64Mi"
  dnsPolicy: ClusterFirst
  restartPolicy: Always
  ```

<br>

## Fontes
[^1]: [Kubernetes: Resource Management for Pods and Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)