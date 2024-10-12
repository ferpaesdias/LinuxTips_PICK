# Utilizando o Docker Scout para checar o número de vulnerabilidades

<br>

**Docker Scout** é uma solução para aprimorar proativamente a segurança da cadeia de suprimentos de software. Ao analisar suas imagens, o Docker Scout compila um inventário de componentes, também conhecido como Lista de Materiais de Software (SBOM). O SBOM é comparado a um banco de dados de vulnerabilidades continuamente atualizado para identificar pontos fracos de segurança.

<br>

## Instalação 

<br>

```shell
curl -fsSL https://raw.githubusercontent.com/docker/scout-cli/main/install.sh -o install-scout.sh
sh install-scout.sh
```

<br>

## Como utilizar

Para verificar as vulnerabilidades de uma imagem é só usar o comando abaixo. Tem que estar logado via Docker Login.

```shell
docker scout cves <nome_da_imagem:tag>
```