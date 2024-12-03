# O que são volumes

<br>

## Volumes

Os arquivos em disco em um container são efêmeros, o que apresenta alguns problemas para aplicativos não triviais quando executados em containers. Um problema ocorre quando um container trava ou é interrompido. O estado do container não é salvo, portanto, todos os arquivos que foram criados ou modificados durante a vida útil do container serão perdidos.
Durante uma falha, o kubelet reinicia o container com um estado limpo. 

Outro problema ocorre quando vários containers estão em execução em um pod e precisam compartilhar arquivos. Pode ser um desafio configurar e acessar um sistema de arquivos compartilhado em todos os containers.

A abstração de volume do Kubernetes resolve esses dois problemas. 

<br>

### Background

O Kubernetes oferece suporte a muitos tipos de volumes. Um Pod pode usar qualquer número de tipos de volume simultaneamente.

Os tipos de volumes efêmeros têm a vida útil de um Pod, mas os volumes persistentes existem além da vida útil de um Pod. Quando um Pod deixa de existir, o Kubernetes destrói volumes efêmeros; no entanto, o Kubernetes não destrói volumes persistentes. 

Para qualquer tipo de volume em um determinado Pod, os dados são preservados durante as reinicializações do container.

Basicamente, um volume é um diretório, possivelmente com alguns dados nele, que é acessível aos containers em um Pod. A forma como esse diretório surge, a mídia que o suporta e o conteúdo dele são determinados pelo tipo de volume específico usado.

Para usar um volume, especifique os volumes a serem fornecidos para o Pod em `.spec.volumes` e declare onde montar esses volumes em containers em `.spec.containers[*].volumeMounts`.

Um processo em um container vê uma visualização do sistema de arquivos composta pelo conteúdo inicial da imagem do container, além de volumes (se definidos) montados dentro do container. O processo vê um sistema de arquivos raiz que inicialmente corresponde ao conteúdo da imagem do container. Qualquer gravação nessa hierarquia do sistema de arquivos, se permitida, afetará o que o processo visualiza quando executa um acesso subsequente ao sistema de arquivos.

Os volumes são montados nos caminhos especificados na imagem. Para cada container definido em um Pod, você deve especificar independentemente onde montar cada volume usado pelo container.

Os volumes não podem ser montados em outros volumes. Além disso, um volume não pode conter um link físico para nada em um volume diferente.

<br>

## Saiba mais
[Kubernetes: Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)