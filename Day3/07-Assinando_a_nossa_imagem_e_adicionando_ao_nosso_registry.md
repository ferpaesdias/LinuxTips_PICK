# Assinando  a  nossa  imagem  e  adicionando  ao  nosso  registry

<br>

## [Cosign](https://github.com/sigstore/cosign)
 
Assinando contêineres OCI (e outros artefatos) usando [Sigstore](https://www.sigstore.dev/)!   
A Cosign visa tornar as assinaturas uma infraestrutura invisível.

<br>

### Instalção do Cosign

[Instalação](https://docs.sigstore.dev/cosign/system_config/installation/#with-the-cosign-binary-or-rpmdpkg-package)

```shell
curl -O -L "https://github.com/sigstore/cosign/releases/latest/download/cosign-linux-amd64"
sudo mv cosign-linux-amd64 /usr/local/bin/cosign
sudo chmod +x /usr/local/bin/cosign
```

<br>

### Gerar um par de chaves

[Documentação oficial](https://docs.sigstore.dev/cosign/key_management/signing_with_self-managed_keys/)

Use o comando abaixo para gerar uma par de chaves. Será solicitada uma senha e sua confirmação.
```shell
cosign generate-key-pair
```
Depois que o comando for finalizado foi gerada a chave pública `cosign.pub` e a chave privada `cosign.key`.

<br>

### Assinando imagens 

[Documentação oficial](https://docs.sigstore.dev/cosign/signing/signing_with_containers/)

A imagem já tem que estar no Docker Hub. Ao executar o comando o usuário já deve estar logado em Docker Login.

```shell
cosign sign --key cosign.key nome_usuario_docker_hub/nome_da_images:tag
```
Será solicitada a senha usada quando foram geradas as chaves.
Digite `y` e depois `Enter` informando que você concorda com os termos.

<br>

### Verificar uma image assinada

Verificando se uma imagem está assinada.

```shell
cosign verify --key cosign.pub nome_usuario_docker_hub/nome_da_images:tag
```

<br>

> [!IMPORTANTE]
> A chave privada não deve ser compartilhada com terceiros em hipótese alguma.