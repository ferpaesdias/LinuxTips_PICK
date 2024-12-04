# Instalando o containerd

<br>

Comando para instalar e configurar o **containerd**:

```shell
# Instalar o containerd
sudo apt-get update && sudo apt-get install -y apt-transport-https ca-certificates curl gnupg lsb-release

sudo install -m 0755 -d /etc/apt/keyrings

sudo curl -fsSL https://download.docker.com/linux/debian/gpg -o /etc/apt/keyrings/docker.asc

sudo chmod a+r /etc/apt/keyrings/docker.asc

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/debian \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update && sudo apt-get install -y containerd.io


# Configurar o containerd, alterar a opção SystemdCgroup para true
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