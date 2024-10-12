# Conhecendo a App que precisamos transformar em container

<br>

Clone o Github do App:

```shell
git clone https://github.com/badtuxx/giropops-senhas.git
```

<br>

Acesse o diretório do App

```shell
cd giropops-senhas
```

<br>

Instale o pip

```shell
apt install pip
```

<br>

Instale as dependências do Python:

```shell
pip install --no-cache-dir -r requirements.txt
```

<br>

Faça a instalação do Redis e inicie o seu serviço:

```shell
apt install redis
systemctl start redis
```

<br>

Crie a variável de ambiente onde o valor seja o endereço IP ou hostname do host do Redis:

```shell
export REDIS_HOST=localhost
```

<br>

Execute o comando `flask` para iniciar o app:

```shell
flask run --host=0.0.0.0
```
