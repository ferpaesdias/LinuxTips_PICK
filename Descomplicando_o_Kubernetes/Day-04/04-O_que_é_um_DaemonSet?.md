# O que é um DaemonSet?

Um **DaemonSet** garante que todos os (ou alguns) *Nodes* executem uma cópia de um *Pod*.

À medida que os *Nodes* são adicionados em um cluster e os *Pods* adicionados aos *Nodes*.

À medida que os *Nodes* são removidos do cluster, os seus *Pods* são coletados com lixo (garbage collected).

Excluir o **DaemonSet** limpará os *Pods* que ele criou.

<br>

Usos típicos de um **DaemonSet**:

- Executar um daemon de armazenamento de cluster em cada Node
- Executar um daemon de coleta de logs em cada Node
- Executar um daemon de monitoramento em cada Node

<br>

## Saiba mais
[Kubernetes: DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/)