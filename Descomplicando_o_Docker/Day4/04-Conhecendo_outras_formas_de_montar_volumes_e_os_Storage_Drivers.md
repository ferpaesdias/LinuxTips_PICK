# Conhecendo outras formas de montar volumes e os Storage Drivers

<br>

### Executando um container com um volume do tipo Volume usando a flag `-v`

```shell
docker container run -d --name container-teste -v volume-teste:/usr/share/nginx/html -p 8080:80 nginx
```

<br>

### Executando um container com um volume somente leitura (readonly) do tipo Volume usando a flag `-v`

```shell
docker container run -d --name container-teste -v volume-teste:/usr/share/nginx/html:ro -p 8080:80 nginx
```

<br>

## Storage Drivers

O Docker usa **Storage Drivers** para armazenar camadas de imagem e dados na camada gravável de um container. A camada gravável de um container não persiste após a exclusão do container, mas é adequada para armazenar dados efêmeros gerados em tempo de execução.

Os **Storage Drivers** são otimizados para eficiência de espaço, mas (dependendo do driver de armazenamento) as velocidades de gravação são inferiores ao desempenho do sistema de arquivos nativo, especialmente para os **Storage Drivers** que usam um sistema de arquivos de cópia na gravação. Aplicativos com uso intensivo de gravação, como armazenamento de banco de dados, são afetados por uma sobrecarga de desempenho, principalmente se existirem dados pré-existentes na camada somente leitura.

Use volumes Docker para dados com uso intensivo de gravação, dados que devem persistir além da vida útil do container e dados que devem ser compartilhados entre containeres. 

<br>

## Selecionar um Storage Driver

<br>

O Docker Engine fornece os seguintes Storage Drivers no Linux:

|Driver|Descrição|
|------|---------|
|`overlay2`|`overlay2` é o Storage Driver preferido para todas as distribuições Linux atualmente suportadas e não requer configuração extra.|
|`fuse-overlayf` | `fuse-overlayfsis` preferido apenas para executar o Rootless Docker em um host antigo que não fornece suporte para overlay2 sem root. O driver fuse-overlayfs não precisa ser usado desde o kernel Linux 5.11, e overlay2 funciona mesmo no modo sem root.|
|`btrfs` e `zfs`| Os Storage Drivers `btrfs` e `zfs` permitem opções avançadas, como a criação de "instantâneos", mas exigem mais manutenção e configuração. Cada um deles depende da configuração correta do sistema de arquivos de apoio.|
|`vfs` | O Storage Driver `vfs` destina-se a fins de teste e a situações em que nenhum sistema de arquivos de cópia na gravação pode ser usado. O desempenho deste driver de armazenamento é ruim e geralmente não é recomendado para uso em produção.|


<br>

## Fontes
[Docker: Storage drivers](https://docs.docker.com/engine/storage/drivers/)   
[Docker: Select a storage driver](https://docs.docker.com/engine/storage/drivers/select-storage-driver/)


