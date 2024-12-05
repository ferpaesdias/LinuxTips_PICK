# PV - PersistentVolume

<br>

O gerenciamento do armazenamento é um problema diferente do gerenciamento de instâncias de computação. O subsistema **PersistentVolume** fornece uma API para usuários e administradores que abstrai detalhes de como o armazenamento é fornecido a partir de como ele é consumido. Para fazer isso, apresentamos dois novos recursos de API: **PersistentVolume** e **PersistentVolumeClaim**.

Um **PersistentVolume** (PV) é uma parte do armazenamento no cluster que foi provisionado por um administrador ou provisionado dinamicamente usando *StorageClass*. É um recurso no cluster assim como um Node é um recurso de cluster.

PVs são plug-ins de volume como Volumes, mas têm um ciclo de vida independente de qualquer Pod individual que use o PV. Este objeto API captura os detalhes da implementação do armazenamento, seja NFS, iSCSI ou um sistema de armazenamento específico do provedor de nuvem.

<br>


## Tipos de PersistentVolume

- `csi`: vContainer Storage Interface (CSI) define uma interface padrão para sistemas de orquestração de contêineres (como Kubernetes) para expor sistemas de armazenamento arbitrários às suas cargas de trabalho de contêiner.

- `fc`: Um tipo de volume `fc` permite que um volume de armazenamento em bloco *Fibre Channel* existente seja montado em um Pod. É possível especificar nomes mundiais (WWNs) de destino únicos ou múltiplos usando o parâmetro `targetWWNs` na configuração do volume. Se vários WWNs forem especificados, os `targetWWNs` esperam que esses WWNs sejam de conexões de vários caminhos.

- `HostPath`: HostPath volume (Somente Nodes). Um PersistentVolume `hostPat` usa um arquivo ou diretório no Node para emular o armazenamento conectado à rede.

- `iscsi`: Um volume `iscsi` permite que um volume iSCSI (SCSI sobre IP) existente seja montado em seu Pod. Ao contrário do `emptyDir`, que é apagado quando um Pod é removido, o conteúdo de um volume `iscsi` é preservado e o volume é simplesmente desmontado. Isso significa que um volume `iscsi` pode ser pré-preenchido com dados e que os dados podem ser compartilhados entre Pods.

- `local`: Um volume `local` representa um dispositivo de armazenamento local montado, como um disco, partição ou diretório.  
Os volumes locais só podem ser usados como um *PersistentVolume* criado estaticamente. O provisionamento dinâmico não é compatível. Em comparação com os volumes `hostPath`, os volumes locais são usados de maneira durável e portátil, sem agendar manualmente os Pods para os Nodes. O sistema está ciente das restrições do Node do volume observando a afinidade do Node no *PersistentVolume*.   
Contudo, os volumes locais estão sujeitos à disponibilidade do Node subjacente e não são adequados para todas as aplicações. Se um Node não estiver íntegro, o volume local ficará inacessível para o Pod. O Pod que usa esse volume não pode ser executado. Os aplicativos que usam volumes locais devem ser capazes de tolerar essa disponibilidade reduzida, bem como a possível perda de dados, dependendo das características de durabilidade do disco subjacente.

- `nfs`: Um volume `nfs` permite que um compartilhamento NFS (Network File System) existente seja montado em um Pod. Ao contrário do `emptyDir`, que é apagado quando um Pod é removido, o conteúdo de um volume `nfs` é preservado e o volume é simplesmente desmontado. Isso significa que um volume NFS pode ser pré-preenchido com dados e que os dados podem ser compartilhados entre Pods. O NFS pode ser montado por vários gravadores simultaneamente.

<br>

>[!Note]
O `hostPath` só deve ser apenas para testes de Node único; NÃO FUNCIONARÁ em um cluster de vários Nodes; considere usar o volume `local`.

<br>

Os seguintes tipos de *PersistentVolume* estão obsoletos, mas ainda estão disponíveis. Se você estiver usando esses tipos de volume, exceto `flexVolume`, `cephfs` e `rbd`, instale os drivers CSI correspondentes:

- **awsElasticBlockStore** - AWS Elastic Block Store (EBS) 
- **azureDisk** - Azure Disk 
- **azureFile** - Azure File 
- **cinder** - Cinder (OpenStack block storage) 
- **flexVolume** - FlexVolume 
- **gcePersistentDisk** - GCE Persistent Disk 
- **portworxVolume** - Portworx volume 
- **vsphereVolume** - vSphere VMDK volume 

<br>

Versões mais antigas do Kubernetes também suportavam os seguintes tipos *PersistentVolume*:

- **cephfs** - (não disponível a partir da versão v1.31)
- **flocker** - Flocker storage. (não disponível a partir da versão v1.25)
- **photonPersistentDisk** - Photon controller persistent disk. (não disponível a partir da versão v1.15)
- **quobyte** - Quobyte volume. (não disponível a partir da versão v1.25)
- **rbd** - Rados Block Device (RBD) volume (não disponível a partir da versão v1.31)
- **scaleIO** - ScaleIO volume. (não disponível a partir da versão v1.21)
- **storageos** - StorageOS volume. (não disponível a partir da versão v1.25)


<br>

## Manifesto 

Exemplo de manifesto de um objeto *PersistentVolume*:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  labels:
    storage: lento
  name: meu-pv
spec:
  capacity: 
    storage: 1Gi
  accessModes: 
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath: 
    path: /mnt/data
  storageClassName: meupv
  ```

<br>

## Saiba mais
[Kubernetes: Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)    
[Kubernetes: Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)
