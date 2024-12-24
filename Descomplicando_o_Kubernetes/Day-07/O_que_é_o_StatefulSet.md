# O que é StatefulSet

<br>

Um **StatefulSet** executa um grupo de Pods e mantém uma identidade fixa para cada um desses Pods. Isso é útil para gerenciar aplicativos que precisam de armazenamento persistente ou de uma identidade de rede estável e exclusiva.

**StatefulSet** é o objeto da API de workload usado para gerenciar aplicativos com estado.

Gerencia a implantação e o escalonamento de um conjunto de Pods e fornece garantias sobre a ordem e a exclusividade desses Pods.

Assim como uma implantação, um **StatefulSet** gerencia Pods baseados em especificações de container idênticas. Ao contrário de uma implantação, um **StatefulSet** mantém uma identidade fixa para cada um de seus Pods. Esses Pods são criados a partir da mesma especificação, mas não são intercambiáveis: cada um tem um identificador persistente que mantém durante qualquer reagendamento.

Se quiser usar volumes de armazenamento para fornecer persistência para sua carga de trabalho, você poderá usar um **StatefulSet** como parte da solução. Embora os Pods individuais em um **StatefulSet** sejam suscetíveis a falhas, os identificadores de Pod persistentes facilitam a correspondência dos volumes existentes com os novos Pods que substituem aqueles que falharam.

<br>

## Usando StatefulSets

**StatefulSets** são valiosos para aplicativos que exigem um ou mais dos seguintes itens.

- Identificadores de rede exclusivos e estáveis.
- Armazenamento estável e persistente.
- Implantação e escalonamento ordenados e elegantes.
- Atualizações contínuas ordenadas e automatizadas.

<br>

## Limitações

- O armazenamento de um determinado Pod deve ser provisionado por um *PersistentVolume Provisioner* com base em um *Storage Class* solicitada ou pré-provisionado por um *admin*.

- Excluir e/ou reduzir um **StatefulSet** não excluirá os volumes associados ao **StatefulSet**. Isso é feito para garantir a segurança dos dados, o que geralmente é mais valioso do que uma limpeza automática de todos os recursos **StatefulSet** relacionados.

- Atualmente, os **StatefulSets** exigem que um *Headless Service* seja responsável pela identidade de rede dos Pods. Você é responsável por criar este Service.

- **StatefulSets** não fornece nenhuma garantia de encerramento de Pods quando um **StatefulSet** é excluído. Para obter o encerramento ordenado e elegante dos Pods no **StatefulSet**, é possível reduzir o **StatefulSet** para "0" antes da exclusão.

- Ao usar *Rolling Updates* com a política de gerenciamento de Pod padrão (`OrderedReady`), é possível entrar em um estado quebrado que requer intervenção manual para reparo.

<br>

## Saiba mais
[Kubernetes: StatefulSets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)   