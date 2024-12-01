# Instalando o containerd

<br>

Comando para instalar e configurar o **containerd**:

```shell
# Instalar o containerd
sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update && sudo apt-get install -y containerd.io


# Configurar o containerd
sudo containerd config default | sudo tee /etc/containerd/config.toml

sudo sed -i 's/SystemdCgroup = false/SystemdCgroup = true/g' /etc/containerd/config.toml

sudo systemctl restart containerd
sudo systemctl status containerd


# Habilitar o serviço do kubelet
sudo systemctl enable --now kubelet
```

<br>

## Saiba mais
[Docker: Install Docker Engine](https://docs.docker.com/engine/install/)   
[Kubernetes: Container Runtimes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)   