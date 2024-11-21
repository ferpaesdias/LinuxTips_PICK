# O que é um Pod?

**Pods** são as menores unidades de computação ​​que você pode criar e gerenciar no Kubernetes.

O contexto compartilhado de um **Pod** é um conjunto de namespaces do Linux, cgroups e potencialmente outras facetas de isolamento – as mesmas coisas que isolam um container. Dentro do contexto de um **Pod**, os aplicativos individuais podem ter outros sub-isolamentos aplicados.

Um **Pod** é semelhante a um conjunto de containers com namespaces e volumes de sistema de arquivos compartilhados.

Os **Pods** em um cluster Kubernetes são usados ​​de duas maneiras principais:

- **Pods que executam um único container**: O modelo “um container por Pod” é o caso de uso mais comum do Kubernetes; nesse caso, você pode pensar em um **Pod** como um wrapper em torno de um único container; O Kubernetes gerencia Pods em vez de gerenciar containers diretamente.

- **Pods que executam vários containers que precisam trabalhar juntos**: Um **Pod** pode encapsular um aplicativo composto de vários containers colocados no mesmo local que estão fortemente acoplados e precisam compartilhar recursos. Esses containers co-localizados formam uma única unidade coesa.

Agrupar vários containers co-localizados e co-gerenciados em um único **Pod** é um caso de uso relativamente avançado. Você deve usar esse padrão apenas em instâncias específicas em que seus containers estão fortemente acoplados.

<br>

## Saiba mais
[Kubernetes: Pods](https://kubernetes.io/docs/concepts/workloads/pods/)