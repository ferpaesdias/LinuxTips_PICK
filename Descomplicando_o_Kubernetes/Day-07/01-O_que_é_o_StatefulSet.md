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

## Identidade do Pod

Os Pods StatefulSet têm uma identidade exclusiva que consiste em um numeração em sequência (ordinal), uma identidade de rede estável e armazenamento estável. A identidade permanece no Pod, independentemente do Node em que ela está (re)agendada.

<br>

### Índice Ordinal

Para um StatefulSet com N réplicas, cada Pod no StatefulSet receberá um ordinal inteiro, que é exclusivo no conjunto. Por padrão, os Pods receberão ordinais de 0 a N-1. O controlador StatefulSet também adicionará um rótulo de Pod com este índice: `apps.kubernetes.io/pod-index`.

<br>

## Stable Network ID (ID de rede estável)

Cada Pod em um StatefulSet deriva seu hostnome do nome do StatefulSet e do ordinal do Pod. O padrão para o hostname construído é `$(statefulset name)-$(ordinal)`. Por exemplo, um StatefulSet de nome `web` e configurado para gerar 03 réplicas criará três Pods denominados `web-0`,`web-1`,`web-2`.

Um StatefulSet pode usar um serviço **Headless** para controlar o domínio de seus Pods. O domínio gerenciado por este Service assume o formato: `$(nome do serviço).$(namespace).svc.cluster.local`, onde "cluster.local" é o domínio do cluster. À medida que cada Pod é criado, ele obtém um subdomínio DNS correspondente, no formato: `$(podname).$(governing service domain)`, onde o "governing service" é definido pelo campo `serviceName` no StatefulSet.

Dependendo de como o DNS está configurado no seu cluster, talvez você não consiga procurar imediatamente o nome DNS de um Pod recém-executado. Esse comportamento pode ocorrer quando outros clientes no cluster já enviaram consultas para o nome do host do Pod antes de ele ser criado. O cache negativo (normal no DNS) significa que os resultados de pesquisas anteriores com falha são lembrados e reutilizados, mesmo depois que o Pod estiver em execução, por pelo menos alguns segundos.

<br>

Se precisar descobrir os Pods imediatamente após eles serem criados, você tem algumas opções:

- Consulte o Kubernetes API diretamente (por exemplo, usando um watch) em vez de depender de pesquisas de DNS.
- Diminua o tempo de armazenamento em cache em seu provedor DNS do Kubernetes (normalmente, isso significa editar o config map do CoreDNS, que atualmente armazena em cache por 30 segundos).

Conforme mencionado na seção de limitações, você é responsável por criar o Headless Service responsável pela identidade de rede dos Pods.

<br>

Aqui estão alguns exemplos de opções de Cluster Domain, Service Name, StatefulSet Name e como isso afeta os nomes DNS dos Pods do StatefulSet.

| Cluster Domain | Service (ns/name) | StatefulSet (ns/name) |	StatefulSet Domain | Pod DNS |	Pod Hostname |
|:-:|:-:|:-:|:-:|:-:|:-:|
| cluster.local | default/nginx | default/web | nginx.default.svc.cluster.local | web-{0..N-1}.nginx.default.svc.cluster.local | web-{0.. N-1} |
| cluster.local | foo/nginx | foo/web | nginx.foo.svc.cluster.local | web-{0..N-1}.nginx.foo.svc.cluster.local | web-{0..N-1} |
| kube.local | foo/nginx | foo/web | nginx.foo.svc.kube.local | web-{0..N-1}.nginx.foo.svc.kube.local | web-{0..N-1} |

<br>

## Armazenamento estável

Para cada entrada VolumeClaimTemplate definida em um StatefulSet, cada Pod recebe um PersistentVolumeClaim.

Se nenhum StorageClass for especificado, o StorageClass padrão será usado. Quando um Pod é (re)agendado em um Node, seus volumeMounts montam os PersistentVolumes associados às suas declarações PersistentVolume. Observe que os PersistentVolumes associados às declarações PersistentVolume dos Pods não são excluídos quando os Pods ou StatefulSet são excluídos. Isso deve ser feito manualmente.

<br>

## Pod Name Label
Quando o controlador StatefulSet cria um Pod, ele adiciona um Label, `statefulset.kubernetes.io/pod-name`, que é definido como o nome do Pod. Este Label permite anexar um serviço a um Pod específico no StatefulSet.

<br>

## Pod Index Label 

<br>

> [!Note]
> Kubernetes v1.32 [stable]  
> Habilitado por padrão: true

<br>

Quando o controlador StatefulSet cria um Pod, o novo Pod é rotulado com `apps.kubernetes.io/pod-index`. O valor deste Label é o índice ordinal do Pod. Esse Label permite rotear o tráfego para um índice de Pod específico, filtrar logs/métricas usando o Label de índice de Pod e muito mais.

Observe que o recurso `PodIndexLabel` está habilitado e bloqueado por padrão para este recurso, para desativá-lo, os usuários terão que usar a versão emulada do servidor v1.31.

<br>

## Garantias de implantação e escalonamento

<br>

- Para um StatefulSet com N réplicas, quando os Pods estão sendo implantados, eles são criados sequencialmente, na ordem de {0..N-1}.

- Quando os Pods são excluídos, eles são encerrados na ordem inversa, de {N-1..0}.

- Antes de uma operação de escalabilidade ser aplicada a um Pod, todos os seus antecessores devem estar em execução e prontos.

- Antes de um Pod ser encerrado, todos os seus sucessores devem ser completamente desligados.

<br>

O StatefulSet não deve especificar um `Pod.Spec.TerminationGracePeriodSeconds` de 0. Esta prática não é segura e é fortemente desencorajada. 

Por exemplo, um StatefulSet de nome `web` e configurado para gerar 03 réplicas, três Pods serão implantados na ordem `web-0`, `web-1`, `web-2`.   
O `web-1` não será implantado antes que `web-0` esteja em execução e pronto, e `web-2` não será implantado até que `web-1` esteja em execução e pronto. Se o `web-0` falhar, depois que o `web-1` estiver em execução e pronto, mas antes do `web-2` ser iniciado, o `web-2` não será iniciado até que o `web-0` seja reiniciado com êxito e se torne em execução e pronto.

Se um usuário dimensionasse o exemplo implantado corrigindo o StatefulSet de forma que réplicas=1, o `web-2` seria encerrado primeiro. `web-1` não seria encerrado até que `web-2` fosse totalmente encerrado e excluído. Se o `web-0` falhasse depois que o `web-2` fosse encerrado e completamente desligado, mas antes do encerramento do `web-1`, o `web-1` não seria encerrado até que o `web-0` estivesse em execução e pronto.

<br>

### Políticas de gerenciamento de Pods

StatefulSet permite que você relaxe suas garantias de pedido enquanto preserva sua exclusividade e garantias de identidade por meio de seu campo `.spec.podManagementPolicy`.

<br>

### Gerenciamento de Pods OrderedReady

O gerenciamento de Pod `OrderedReady` é o padrão para StatefulSets. Ele implementa o comportamento descrito acima.

<br>

### Gerenciamento paralelo de Pods

O gerenciamento paralelo de Pods informa ao controlador StatefulSet para iniciar ou encerrar todos os Pods em paralelo e não esperar que os Pods fiquem em execução e prontos ou completamente encerrados antes de iniciar ou encerrar outro Pod. Esta opção afeta apenas o comportamento das operações de escalabilidade. As atualizações não são afetadas.



<br>

## Saiba mais
[Kubernetes: StatefulSets](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/)   


Por exemplo, um StatefulSet de nome `web` e configurado para gerar 03 réplicas criará três Pods denominados `web-0`,`web-1`,`web-2`.