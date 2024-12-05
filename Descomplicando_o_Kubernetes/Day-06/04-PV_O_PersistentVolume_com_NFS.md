# O PersistentVolume com NFS

<br>

## Criando um servidor NFS

<br>

Criando um servidor NFS para testar o PersistentVolume com NFS

```shell
# Instalando apps necessários para a configuração do NFS (Debian)
sudo apt install nfs-kernel-server nfs-common

# Criando o diretório do compartilhamento NFS
sudo mkdir /mnt/nfs

# Configurar um usuário comum como proprietário do diretório
sudo chown usuario.usuario /mnt/nfs

# Configurando o NFS
sudo vim /etc/exports

# Adicione a seguinte linha no final do arquivo /etc/exports. Se desejar, troque o asterisco pelo range de IP da sua rede
/mnt/nfs        *(rw,sync,no_root_squash,no_subtree_check)

# Informe que o arquivo /etc/exports foi alterado
sudo exportfs -ar

# Verifique se o NFS está montado corretamente
showmount -e
```

<br>

## Exemplo de manifesto de um PersistentVolume com NFS

<br>

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  labels:
    storage: nfs
  name: meu-pv-nfs
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  nfs:
    server: 192.168.3.24
    path: "/mnt/nfs"
  storageClassName: meu-pv-nfs
```
