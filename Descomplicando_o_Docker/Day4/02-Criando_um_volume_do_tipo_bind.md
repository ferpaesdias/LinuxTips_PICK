# Criando um volume do tipo bind[^1]

Os volumes do tipo **bind** existem desde os primeiros dias do Docker. Os volumes **bind** têm funcionalidades limitadas em comparação com os volumes do tipo **volume**. Quando você usa um volume **bind**, um arquivo ou diretório na máquina host é montado em um container. O arquivo ou diretório é referenciado por seu caminho absoluto na máquina host.

O arquivo ou diretório já não precisa existir no host Docker. Ele é criado sob demanda, caso ainda não exista. Os volumes **bind** têm muito desempenho, mas dependem do sistema de arquivos da máquina host ter uma estrutura de diretório específica disponível. Se você estiver desenvolvendo novos aplicativos Docker, considere usar os volumes do tipo **volume**. Você não pode usar comandos Docker CLI para gerenciar diretamente os volumes do tipo **bind**.

<br>

## Escolha da flag `-v` ou `--mount`

<br>

Em geral, a flag `--mount` é mais explícita e detalhada. A maior diferença é que a sintaxe `-v` combina todas as opções em um campo, enquanto a sintaxe `--mount` as separa. Aqui está uma comparação da sintaxe de cada sinalizador.

>Dica
>
> Novos usuários devem usar a sintaxe `--mount`. Usuários experientes podem estar mais familiarizados com a sintaxe `-v` ou `--volume`, mas são encorajados a usar `--mount`, porque a pesquisa mostrou que é mais fácil de usar.

<br>

- `-v` ou `--volume`: Consiste em três campos, separados por dois pontos (:). Os campos devem estar na ordem correta e o significado de cada campo não é imediatamente óbvio.

    -  No caso de volumes **bind**, o primeiro campo é o caminho para o arquivo ou diretório na máquina host.
    - O segundo campo é o caminho onde o arquivo ou diretório está montado no container.
    - O terceiro campo é opcional e é uma lista de opções separadas por vírgulas, como `ro`, `z` e `Z`. 

<br>

- `--mount`: Consiste em vários pares de valores-chave, separados por vírgulas e cada um consistindo em uma tupla `<key=<value>`. A sintaxe `--mount` é mais detalhada que `-v` ou `--volume`, mas a ordem das chaves não é significativa e o valor do sinalizador é mais fácil de entender.

    - `type`: Pode ser `bind`, `volume` ou `tmpfs`. 
    - `source`: Para volumes **bind**, este é o caminho para o arquivo ou diretório no host. Pode ser especificado como `source` ou `src`.
    - `destination`: O caminho onde o arquivo ou diretório está montado no container. Pode ser especificado como `destination`, `dst` ou `target`.
    - A opção `readonly`, se presente, faz com que um volume `bind` seja [**montada no contêiner como somente leitura**](https://docs.docker.com/engine/storage/bind-mounts/#use-a-read-only-bind-mount). Pode ser especificado como `ro`.
    - A opção `bind-propagation`, se presente, altera a opção **[bind-propagation](https://docs.docker.com/engine/storage/bind-mounts/#configure-bind-propagation)**. Pode ser `rprivado`, `private`, `rshared`, `shared`, `rslave`, `slave`.
    - A flag `--mount` não suporta opções `z` ou `Z` para modificar labels **SELinux**.


<br>

## Diferenças entre o comportamento das flags `-v` ou `--mount`

<br>

Como as flags `-v` e `--volume` fazem parte do Docker há muito tempo, seu comportamento não pode ser alterado. Isso significa que existe um comportamento diferente entre `-v` e `--mount`.

Se você usar `-v` ou `--volume` para montar um arquivo ou diretório que ainda não existe no host Docker, `-v` criará o endpoint para você. É sempre criado como um diretório.

Se você usar `--mount` para montar um arquivo ou diretório que ainda não existe no host do Docker, o Docker não o criará automaticamente para você, mas gerará um erro.

<br>

## Iniciando um contêiner com volume do tipo bind

<br>

Usando a flag `--mount`:

```shell
$ docker run -d -it --name teste-volume \
  --mount type=bind,source="$(pwd)"/app,target=/app,ro \
  debian:11
```
 
<br>

Usando a flag `-v` ou `--volume`:

```shell
$ docker run -d -it --name teste-volume \
  -v "$(pwd)"/app:/app,ro \
  debian:11
```

<br>

## Fontes
[^1]: [Bind mounts](https://docs.docker.com/engine/storage/bind-mounts/)

