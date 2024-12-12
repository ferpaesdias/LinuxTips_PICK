# O StorageClass

<br>

Um **StorageClass** fornece uma maneira para os administradores descreverem as classes de armazenamento que oferecem.

Classes diferentes podem ser mapeadas para níveis de qualidade de serviço, ou para políticas de backup, ou para políticas arbitrárias determinadas pelos administradores de cluster. O próprio Kubernetes não tem opinião sobre o que as classes representam.

O conceito de classe de armazenamento do Kubernetes é semelhante aos “perfis” em alguns outros designs de sistema de armazenamento.

<br>

## Objetos StorageClass

Cada **StorageClass** contém os campos `provisioner`, `parameter` e `reclaimPolicy`, que são usados ​​quando um *PersistentVolume* pertencente à classe precisa ser provisionado dinamicamente para satisfazer um *PersistentVolumeClaim* (PVC).

O nome de um objeto **StorageClass** é significativo e é como os usuários podem solicitar uma classe específica. Os administradores definem o nome e outros parâmetros de uma classe ao criar pela primeira vez objetos **StorageClass**.

Como administrador, você pode especificar um **StorageClass** padrão que se aplique a qualquer PVC que não solicite uma classe específica.

<br>

## StorageClass default

Você pode marcar um StorageClass como padrão para seu cluster. 

Quando um PVC não especifica um storageClassName, o StorageClass padrão é usado.

Se você definir a anotação `storageclass.kubernetes.io/is-default-class` como true em mais de um StorageClass em seu cluster e, em seguida, criar um PersistentVolumeClaim sem nenhum `storageClassName` definido, o Kubernetes usará o StorageClass padrão criado mais recentemente.

<br>

## Provisioner (provisionador)

Cada *StorageClass* possui um **provisioner** que determina qual plug-in de volume é usado para provisionar PVs. Este campo deve ser especificado.

Você não está restrito a especificar os provisionadores "internos" listados aqui (cujos nomes são prefixados com "kubernetes.io" e enviados junto com o Kubernetes). Você também pode executar e especificar provisionadores externos, que são programas independentes que seguem uma especificação definida pelo Kubernetes.

Os autores de provisionadores externos têm total discrição sobre onde seu código reside, como o provisionador é enviado, como ele precisa ser executado, qual volume de plugin ele usa (incluindo Flex), etc. O repositório [kubernetes-sigs/sig-storage-lib-external-provisioner](https://github.com/kubernetes-sigs/sig-storage-lib-external-provisioner) abriga uma biblioteca para escrever provisionadores externos que implementa a maior parte da especificação. 

<br>

### Lista de provisionadores 

Lista de provisionadores e seus provedores

- `kubernetes.io/aws-ebs`: AWS Elastic Block Store (EBS)
- `kubernetes.io/azure-disk`: Azure Disk
- `kubernetes.io/gce-pd`: Google Compute Engine (GCE)  Persistent Disk
- `kubernetes.io/cinder`: OpenStack Cinder
- `kubernetes.io/vsphere-volume`: vSphere
- `kubernetes.io/no-provisioner`: Volumes locais
- `kubernetes.io/host-path`: Volumes locais

<br>

## Manifesto

Exemplo de manifesto de um StorageClass

```shell
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: nfs
  labels:
    storage: nfs
provisioner: nfs.csi.k8s.io
reclaimPolicy: Retain
volumeBindingMode: WaitForFirstConsumer
```

<br>

## Comandos

Listar StorageClass
```shell
kubectl get storageclass
```

<br>

Obter detalhes de um determinado StorageClass
```shell
kubectl describe storageclass sc-exemplo
```

<br>

## Saiba mais
[Kubernetes: Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)