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

## Instalando o NFS CSI driver for Kubernetes

No Node Control Plane execute os comandos abaixo para instalar o **NFS CSI driver for Kubernetes**:

```shell
curl -skSL https://raw.githubusercontent.com/kubernetes-csi/csi-driver-nfs/v4.9.0/deploy/install-driver.sh | bash -s v4.9.0 --
```

<br>

Verifique se os Pods com o prefixo `csi-nfs` foram criados:
```shell
kubectl -n kube-system get pod -o wide -l app=csi-nfs-controller
kubectl -n kube-system get pod -o wide -l app=csi-nfs-node
```

<br>

Exemplo da saída do comando:
```shell
NAME                                 READY   STATUS    RESTARTS   AGE     IP              NODE                  NOMINATED NODE   READINESS GATES
csi-nfs-controller-75b74fd4f-zc7h9   4/4     Running   0          2m41s   192.168.3.203   kubernetes03-node02   <none>           <none>
csi-nfs-node-6zk6k   3/3     Running   0          2m41s   192.168.3.202   kubernetes02-node01   <none>           <none>
csi-nfs-node-rvn94   3/3     Running   0          2m41s   192.168.3.203   kubernetes03-node02   <none>           <none>
csi-nfs-node-wz9hz   3/3     Running   0          2m41s   192.168.3.201   kubernetes01-server   <none>           <none>
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
  name: pv-nfs
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs
  mountOptions:
    - nfsvers=4.1
  csi:
    driver: nfs.csi.k8s.io
    volumeHandle: Kubernetes04-NFS.kubernetes.local/mnt/nfs
    volumeAttributes:
      server: Kubernetes04-NFS.kubernetes.local
      share: /mnt/nfs
```

<br>

## Saiba mais
[Kubernetes: Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)   
[Kubernetes: Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)   
[Kubernetes: Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)   
[GitHub: NFS CSI driver for Kubernetes](https://github.com/kubernetes-csi/csi-driver-nfs)   