# Usando o Trivy para verificar vulnerabilidades e como ter uma imagem com 0 vulnerabilidades

<br>

## Trivy

<br>

O [Trivy](https://trivy.dev/) é um scanner de segurança abrangente e versátil. Ele possui scanners que procuram problemas de segurança e aponta onde pode encontrar esses problemas.

O scanner do Trivy inclui:
- Pacotes de sistema operacional e dependências de software em uso (SBOM)[^1]
- Vulnerabilidades conhecidas (CVEs)[^2]
- Problemas e configurações incorretas de IaC
- Informações confidenciais e segredos
- Licenças de software


## Instalação do Trivy

<br>

Debian/Ubuntu (Official)
```shell
sudo apt-get install wget apt-transport-https gnupg
wget -qO - https://aquasecurity.github.io/trivy-repo/deb/public.key | gpg --dearmor | sudo tee /usr/share/keyrings/trivy.gpg > /dev/null
echo "deb [signed-by=/usr/share/keyrings/trivy.gpg] https://aquasecurity.github.io/trivy-repo/deb generic main" | sudo tee -a /etc/apt/sources.list.d/trivy.list
sudo apt-get update
sudo apt-get install trivy

```
ou 
[Instalação do Trivy](https://aquasecurity.github.io/trivy/v0.56/getting-started/installation/)


<br>

## Como usar

Faça a varredura na imagem conforme o comando abaixo:

```shell
trivy image <nome_da_imagem:tag>
```

<br>

Caso não esteja usando o usuário root e o Trivy apresente uma mensagem de erro de permissão de socket, experimente fazer conforme abaixo.

Primeiro, verifique o contexto do Docker que o seu usuário está usando. O `*` indica qual é o contexto utilizado. Neste caso, é o `rootless`.

```shell
docker context ls
NAME         DESCRIPTION                               DOCKER ENDPOINT                     ERROR
default      Current DOCKER_HOST based configuration   unix:///var/run/docker.sock         
rootless *   Rootless mode                             unix:///run/user/1000/docker.sock 
```

<br>

Copie o caminho do `DOCKER ENDPOINT` do contexto utilizado e o use junto com o comando do Trivy como está abaixo:

```shell
trivy image --docker-host unix:///run/user/1000/docker.sock <nome_da_imagem:tag>
```


<br>
<br>
<br>


## Fonte
[^1]: [What is a Software Bill of Materials (SBOM)?](https://www.crowdstrike.com/cybersecurity-101/secops/software-bill-of-materials-sbom/)  Um SBOM (Software Bill of Materials) é uma lista abrangente de todos os componentes de software, dependências e metadados associados a um aplicativo.    
[^2]: [O que é CVE?](https://www.redhat.com/pt-br/topics/security/what-is-cve)  O CVE, sigla inglesa para vulnerabilidades e exposições comuns, é uma lista pública de falhas de segurança. 