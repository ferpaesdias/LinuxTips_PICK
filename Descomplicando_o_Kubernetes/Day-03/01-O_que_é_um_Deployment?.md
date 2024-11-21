# O que é um deployment?

Um **Deployment** gerencia um conjunto de Pods para executar um workload, normalmente um que não mantém o estado (stateless).

Você descreve o estado desejado em um **Deployment** e o **Deployment Controller** altera o estado atual para o estado desejado em uma taxa controlada.

Você pode definir **Deployment** para criar novos *ReplicaSets* ou para remover **Deployments** existentes e adotar todos os novos recursos com novos **Deployments**.

<br>

>[!Note]
Não gerencie *ReplicaSets* pertencentes a um **Deployment**. Considere abrir uma *issue* no repositório principal do Kubernetes se o seu caso de uso não for abordado abaixo.

<br>

## Casos de uso

O Casos de Uso típicos para **Deployments**:

- **Crie um Deployment para implementar um ReplicaSet**: O *ReplicaSet* cria Pods em *background*. E, verifica se o status da implementação foi bem-sucedida ou não.

- **Declare um novo estado para os Pods** atualizando o *PodTemplateSpec* de um **Deployment**. Um novo *ReplicaSet* é criado e o **Deployment** gerencia movendo os Pods do antigo *ReplicaSet* para um novo em uma taxa controlada. Cada novo *ReplicaSet* atualiza a revisão do **Deployment**.

- **Rollback para uma revisão de Deployment anterior**: se o atual estado de um **Deployment** não está estável. Cada rollback atualiza a revisão de um **Deployment**.

- **Faça scale up do Deployment para suportar mais carga.**

- **Pause a implementação de um Deployment** para aplicar múltiplas correções para o seu *PodTemplateSec* e, em seguida, retome-o para iniciar uma noca implementação.

- **Use o status do Deployment** como um indicador de que uma implementação travou.

- **Limpe ReplicaSets mais antigos** que não são mais necessários.

<br>

## Saiba mais
[Kubernetes: Pods](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#creating-a-deployment)