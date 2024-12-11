# O PersistentVolumeClaim (PVC)

<br>

Um **PersistentVolumeClaim** (PVC) é uma solicitação de armazenamento feita por um usuário. É semelhante a um Pod. Os Pods consomem recursos do Node e os PVCs consomem recursos de um *PersistentVolume* (PV).

Os Pods podem solicitar níveis específicos de recursos (CPU e memória). As declarações podem solicitar tamanhos e modos de acesso específicos (por exemplo, podem ser montadas como *ReadWriteOnce*, *ReadOnlyMany*, *ReadWriteMany* ou *ReadWriteOncePod*).

Embora **PersistentVolumeClaim** permitam que um usuário consuma recursos de armazenamento abstratos, é comum que os usuários precisem de PersistentVolumes com propriedades variadas, como desempenho, para diferentes problemas. Os administradores de cluster precisam ser capazes de oferecer uma variedade de PersistentVolumes que diferem em mais aspectos do que tamanho e modos de acesso, sem expor os usuários aos detalhes de como esses volumes são implementados. Para essas necessidades existe o recurso *StorageClass*.

<br>

## Ciclo de vida de um Volume e um Claim

PVs são recursos no cluster. Os PVCs são solicitações para esses recursos e também atuam como verificações de declarações para o recurso. A interação entre PVs e PVCs segue este ciclo de vida:

<br>

### Provisionamento

Existem duas maneiras pelas quais os PVs podem ser provisionados: **estaticamente** ou **dinamicamente**.

<br>

#### Estaticamente

Um administrador de cluster cria vários PVs. Eles carregam os detalhes do armazenamento real, que está disponível para uso pelos usuários do cluster. Eles existem na API Kubernetes e estão disponíveis para consumo.

<br>

#### Dinamicamente

Quando nenhum dos PVs estáticos criados pelo administrador corresponder ao **PersistentVolumeClaim** de um usuário, o cluster poderá tentar provisionar dinamicamente um volume especialmente para o PVC. Este provisionamento é baseado em **StorageClasses**: o PVC deve solicitar uma *StorageClasses* e o administrador deve ter criado e configurado essa classe para que ocorra o provisionamento dinâmico. As declarações que solicitam a classe `""` desabilitam efetivamente o provisionamento dinâmico para si mesmas.

Para ativar o provisionamento de armazenamento dinâmico com base na *StorageClasses*, o administrador do cluster precisa ativar o controlador de admissão `DefaultStorageClass` no API Server. Isso pode ser feito, por exemplo, garantindo que `DefaultStorageClass` esteja entre a lista ordenada e delimitada por vírgulas de valores para o sinalizador `--enable-admission-plugins` do componente do API Server. 

<br>

### Binding

Um usuário cria, ou no caso de provisionamento dinâmico, já criou, um **PersistentVolumeClaim** com uma quantidade específica de armazenamento solicitada e com determinados modos de acesso. Um loop de controle no Control Plane procura novos PVCs, encontra um PV correspondente (se possível) e os une. Se um PV foi provisionado dinamicamente para um novo PVC, o loop sempre vinculará esse PV ao PVC. Caso contrário, o usuário sempre obterá pelo menos o que pediu, mas o volume poderá ser superior ao solicitado. Depois de vinculadas, as vinculações de **PersistentVolumeClaim** são exclusivas, independentemente de como foram vinculadas. Uma ligação PVC para PV é um mapeamento um para um, usando um *ClaimRef* que é uma ligação bidirecional entre **PersistentVolume** e **PersistentVolumeClaim**.

As reivindicações permanecerão desvinculadas indefinidamente se não existir um volume correspondente. As reivindicações serão vinculadas à medida que os volumes correspondentes estiverem disponíveis. Por exemplo, um cluster provisionado com muitos PVs de 50Gi não corresponderia a um PVC solicitando 100Gi. O PVC pode ser vinculado quando um PV de 100Gi é adicionado ao cluster.

<br>

### Using

Os Pods usam declarações como volumes. O cluster inspeciona a declaração para encontrar o volume vinculado e monta esse volume para um Pod. Para volumes que suportam vários modos de acesso, o usuário especifica qual modo deseja ao usar sua declaração como um volume em um Pod.

Depois que um usuário tiver uma reivindicação e essa reivindicação estiver vinculada, o PV vinculado pertencerá ao usuário pelo tempo que ele precisar. Os usuários agendam Pods e acessam seus PVs reivindicados incluindo uma seção **persistenteVolumeClaim** no bloco de volumes de um Pod.

<br>

### Storage Object em Use Protection

O objetivo do **Use Protection** de um **Storage Object** em uso é garantir que *PersistentVolumeClaims* (PVCs) em uso ativo por um Pod e *PersistentVolume* (PVs) vinculados a PVCs não sejam removidos do sistema, pois isso pode resultar em perda de dados.

Se um usuário excluir um PVC em uso ativo por um Pod, o PVC não será removido imediatamente. A remoção do PVC é adiada até que o PVC não seja mais usado ativamente por nenhum Pod. Além disso, se um administrador excluir um PV vinculado a um PVC, o PV não será removido imediatamente. A remoção do PV é adiada até que o PV não esteja mais ligado a um PVC.

<br>


## Exemplo do manifesto de um objeto Persistent Volume Claim

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-nfs
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: nfs
  selector:
    matchLabels:
      storage: nfs
```
Descrição dos campos

- `spec.accessModes`: Define os modos de acesso que cada PV terá:
    - `ReadWriteOnce` (RWO): O volume pode ser montado como leitura e gravação por um único Node. O modo de acesso `ReadWriteOnce` ainda pode permitir que vários Pods acessem o volume quando os Pods estão em execução no mesmo Node. 
    - `ReadWriteOncePod` (RWOP): O volume pode ser montado como leitura e gravação por um único Pod. Use o modo de acesso `ReadWriteOncePod` se quiser garantir que apenas um Pod em todo o cluster possa ler esse PVC ou gravar nele.
    - `ReadOnlyMany` (ROX): O volume pode ser montado como somente leitura por muitos Nodes.
    - `ReadWriteMany` (RWX): o volume pode ser montado como leitura e gravação por vários Nodes.

- `spec.resources`: As declarações, como os Pods, podem solicitar quantidades específicas de um recurso. Neste caso, a solicitação é de armazenamento. 

- `spec.storageClassName`: Uma declaração pode solicitar uma classe específica especificando o nome de um `StorageClass` usando o atributo `storageClassName`. Somente PVs da classe solicitada, aqueles com o mesmo `storageClassName` que o PVC, podem ser vinculados ao PVC.

- `spec.selector`: As declarações podem especificar um *label selector* para filtrar ainda mais o conjunto de volumes. Somente os volumes cujos labels correspondem ao selector podem ser vinculados à declaração. O selector pode consistir em dois campos:

    - `matchLabels`: O volume deve ter um label com este valor
    - `matchExpressions`: Uma lista de requisitos feita especificando chave, lista de valores e operador que relaciona a chave e os valores. Os operadores válidos incluem *In*, *NotIn*, *Exists* e *DoesNotExist*.

<br>

## Exemplo de manifesto de um objeto Deployment com um volume NFS

Este manifesto pode ser usado em conjunto com o StorageClass e o PersistentVolume dos arquivos [02-O_StorageClass.md](./02-O_StorageClass.md) e [04-PV_O_PersistentVolume_com_NFS.md](./04-PV_O_PersistentVolume_com_NFS.md), respectivamente.

<br>

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: nginx-deployment
  name: nginx-deployment
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx-deployment
  strategy: {}
  template:
    metadata:
      labels:
        app: nginx-deployment
    spec:
      containers:
      - image: nginx
        name: nginx
        resources:
          limits:
            cpu: 0.5
            memory: 256Mi
          requests:
            cpu: 0.3
            memory: 64Mi
        volumeMounts:
          - name: meu-pvc
            mountPath: /usr/share/nginx/html
      volumes:
        - name: meu-pvc
          persistentVolumeClaim:
            claimName: pvc-nfs
```

<br>

## Saiba mais
[Kubernetes: Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)   
[Kubernetes: Volumes](https://kubernetes.io/docs/concepts/storage/volumes/)   
[Kubernetes: Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)   
[GitHub: NFS CSI driver for Kubernetes](https://github.com/kubernetes-csi/csi-driver-nfs)