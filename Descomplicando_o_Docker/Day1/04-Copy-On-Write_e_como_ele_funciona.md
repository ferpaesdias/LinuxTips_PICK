# A estratégia copy-on-write (CoW)

<br>

**Copy-on-write** é uma estratégia de compartilhamento e cópia de arquivos para máxima eficiência. Se um arquivo ou diretório existir em uma camada inferior da imagem e outra camada (incluindo a camada gravável) precisar de acesso de leitura a ele, ele apenas usará o arquivo existente. Na primeira vez que outra camada precisar modificar o arquivo (ao construir a imagem ou executar o contêiner), o arquivo será copiado para essa camada e modificado. Isso minimiza a E/S e o tamanho de cada uma das camadas subsequentes. 

<br>

## Saiba mais
[Docker: The copy-on-write (CoW) strategy](https://docs.docker.com/engine/storage/drivers/#the-copy-on-write-cow-strategy)   