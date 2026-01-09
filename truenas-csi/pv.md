# Truenas PV backups

- giteaconfig-local-pvc
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  annotations:
    pv.kubernetes.io/provisioned-by: nfs
    volume.kubernetes.io/provisioner-deletion-secret-name: provisioner-secret-nfs-csi-nfs-democratic-csi
    volume.kubernetes.io/provisioner-deletion-secret-namespace: democratic-csi
  creationTimestamp: "2023-12-07T15:45:47Z"
  finalizers:
  - kubernetes.io/pv-protection
  name: pvc-0c6e4d07-d1e1-4db5-a49e-8049d70ba2b0
  resourceVersion: "10495022"
  uid: d08c84ce-68df-40dd-a3d2-952e1e8f40ee
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 2Gi
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: giteaconfig-truenas-pvc
    namespace: gitea
    resourceVersion: "10493611"
    uid: 0c6e4d07-d1e1-4db5-a49e-8049d70ba2b0
  csi:
    controllerExpandSecretRef:
      name: controller-expand-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    controllerPublishSecretRef:
      name: controller-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    driver: nfs
    fsType: nfs
    nodePublishSecretRef:
      name: node-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    nodeStageSecretRef:
      name: node-stage-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    volumeAttributes:
      node_attach_driver: nfs
      provisioner_driver: freenas-api-nfs
      server: 10.0.0.20
      share: /mnt/it-nas-6tb/k8s/volumes/pvc-0c6e4d07-d1e1-4db5-a49e-8049d70ba2b0
      storage.kubernetes.io/csiProvisionerIdentity: 1701794694568-754-nfs
    volumeHandle: pvc-0c6e4d07-d1e1-4db5-a49e-8049d70ba2b0
  mountOptions:
  - noatime
  - nfsvers=4
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs-csi
  volumeMode: Filesystem
status:
  phase: Bound
```

- giteadata-local-pvc
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  annotations:
    pv.kubernetes.io/provisioned-by: nfs
    volume.kubernetes.io/provisioner-deletion-secret-name: provisioner-secret-nfs-csi-nfs-democratic-csi
    volume.kubernetes.io/provisioner-deletion-secret-namespace: democratic-csi
  creationTimestamp: "2023-12-07T15:45:47Z"
  finalizers:
  - kubernetes.io/pv-protection
  name: pvc-0c7a5eb1-0d0d-477d-8ed4-01d295ebf7e7
  resourceVersion: "10495085"
  uid: c562c2b1-5ba8-441f-8b90-38aedfc7b61b
spec:
  accessModes:
  - ReadWriteMany
  capacity:
    storage: 10Gi
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: giteadata-truenas-pvc
    namespace: gitea
    resourceVersion: "10493615"
    uid: 0c7a5eb1-0d0d-477d-8ed4-01d295ebf7e7
  csi:
    controllerExpandSecretRef:
      name: controller-expand-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    controllerPublishSecretRef:
      name: controller-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    driver: nfs
    fsType: nfs
    nodePublishSecretRef:
      name: node-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    nodeStageSecretRef:
      name: node-stage-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    volumeAttributes:
      node_attach_driver: nfs
      provisioner_driver: freenas-api-nfs
      server: 10.0.0.20
      share: /mnt/it-nas-6tb/k8s/volumes/pvc-0c7a5eb1-0d0d-477d-8ed4-01d295ebf7e7
      storage.kubernetes.io/csiProvisionerIdentity: 1701794694568-754-nfs
    volumeHandle: pvc-0c7a5eb1-0d0d-477d-8ed4-01d295ebf7e7
  mountOptions:
  - noatime
  - nfsvers=4
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs-csi
  volumeMode: Filesystem
status:
  phase: Bound
```

- homepage-pvc

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"PersistentVolume","metadata":{"annotations":{"pv.kubernetes.io/bound-by-controller":"yes","pv.kubernetes.io/provisioned-by":"nfs","volume.kubernetes.io/provisioner-deletion-secret-name":"provisioner-secret-nfs-csi-nfs-democratic-csi","volume.kubernetes.io/provisioner-deletion-secret-namespace":"democratic-csi"},"creationTimestamp":"2023-12-31T08:39:19Z","finalizers":["kubernetes.io/pv-protection"],"name":"pvc-10b285e7-f7e7-4818-aed9-276151814f8e","resourceVersion":"38075616","uid":"14144c43-dad8-4350-b0dd-2868567d6ce7"},"spec":{"accessModes":["ReadWriteOnce"],"capacity":{"storage":"5Gi"},"csi":{"controllerExpandSecretRef":{"name":"controller-expand-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"controllerPublishSecretRef":{"name":"controller-publish-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"driver":"nfs","fsType":"nfs","nodePublishSecretRef":{"name":"node-publish-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"nodeStageSecretRef":{"name":"node-stage-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"volumeAttributes":{"node_attach_driver":"nfs","provisioner_driver":"freenas-api-nfs","server":"10.0.0.20","share":"/mnt/it-nas-6tb/k8s/volumes/pvc-10b285e7-f7e7-4818-aed9-276151814f8e","storage.kubernetes.io/csiProvisionerIdentity":"1703083022447-1075-nfs"},"volumeHandle":"pvc-10b285e7-f7e7-4818-aed9-276151814f8e"},"mountOptions":["noatime","nfsvers=4"],"persistentVolumeReclaimPolicy":"Retain","storageClassName":"nfs-csi","volumeMode":"Filesystem"},"status":{"phase":"Available"}}
    pv.kubernetes.io/bound-by-controller: "yes"
    pv.kubernetes.io/provisioned-by: nfs
    volume.kubernetes.io/provisioner-deletion-secret-name: provisioner-secret-nfs-csi-nfs-democratic-csi
    volume.kubernetes.io/provisioner-deletion-secret-namespace: democratic-csi
  creationTimestamp: "2024-04-01T23:19:14Z"
  finalizers:
  - kubernetes.io/pv-protection
  name: pvc-10b285e7-f7e7-4818-aed9-276151814f8e
  resourceVersion: "39158729"
  uid: 9869a28e-cc36-4856-913d-c79c84596f98
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 5Gi
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: homepage-pvc
    namespace: homepage
    resourceVersion: "39158727"
    uid: b3479f76-6e36-48ec-a69e-8fc65f3477f6
  csi:
    controllerExpandSecretRef:
      name: controller-expand-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    controllerPublishSecretRef:
      name: controller-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    driver: nfs
    fsType: nfs
    nodePublishSecretRef:
      name: node-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    nodeStageSecretRef:
      name: node-stage-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    volumeAttributes:
      node_attach_driver: nfs
      provisioner_driver: freenas-api-nfs
      server: 10.0.0.20
      share: /mnt/it-nas-6tb/k8s/volumes/pvc-10b285e7-f7e7-4818-aed9-276151814f8e
      storage.kubernetes.io/csiProvisionerIdentity: 1703083022447-1075-nfs
    volumeHandle: pvc-10b285e7-f7e7-4818-aed9-276151814f8e
  mountOptions:
  - noatime
  - nfsvers=4
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs-csi
  volumeMode: Filesystem
status:
  phase: Bound
```

- embymedia-local-pvc

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  annotations:
    pv.kubernetes.io/provisioned-by: nfs
    volume.kubernetes.io/provisioner-deletion-secret-name: provisioner-secret-nfs-csi-nfs-democratic-csi
    volume.kubernetes.io/provisioner-deletion-secret-namespace: democratic-csi
  creationTimestamp: "2023-10-28T18:54:50Z"
  finalizers:
  - kubernetes.io/pv-protection
  name: pvc-51f7c0cb-8ad7-44c3-a065-b3d283c2da99
  resourceVersion: "10083784"
  uid: b6212ee8-9a57-4d42-9dcd-1b24d7386ef8
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 500Gi
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: embymedia-local-pvc
    namespace: emby
    resourceVersion: "1108166"
    uid: 51f7c0cb-8ad7-44c3-a065-b3d283c2da99
  csi:
    controllerExpandSecretRef:
      name: controller-expand-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    controllerPublishSecretRef:
      name: controller-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    driver: nfs
    fsType: nfs
    nodePublishSecretRef:
      name: node-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    nodeStageSecretRef:
      name: node-stage-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    volumeAttributes:
      node_attach_driver: nfs
      provisioner_driver: freenas-api-nfs
      server: 10.0.0.20
      share: /mnt/it-nas-6tb/k8s/volumes/pvc-51f7c0cb-8ad7-44c3-a065-b3d283c2da99
      storage.kubernetes.io/csiProvisionerIdentity: 1698514144766-2257-nfs
    volumeHandle: pvc-51f7c0cb-8ad7-44c3-a065-b3d283c2da99
  mountOptions:
  - noatime
  - nfsvers=4
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs-csi
  volumeMode: Filesystem
status:
  phase: Bound
```

- emby-local-pvc

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  annotations:
    pv.kubernetes.io/provisioned-by: nfs
    volume.kubernetes.io/provisioner-deletion-secret-name: provisioner-secret-nfs-csi-nfs-democratic-csi
    volume.kubernetes.io/provisioner-deletion-secret-namespace: democratic-csi
  creationTimestamp: "2023-10-28T18:54:50Z"
  finalizers:
  - kubernetes.io/pv-protection
  name: pvc-bb231d3c-a425-46aa-8358-170b4de77709
  resourceVersion: "10083815"
  uid: 0947decf-d59f-4251-afe4-4f4e1d11b5ac
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 10Gi
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: emby-local-pvc
    namespace: emby
    resourceVersion: "1108162"
    uid: bb231d3c-a425-46aa-8358-170b4de77709
  csi:
    controllerExpandSecretRef:
      name: controller-expand-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    controllerPublishSecretRef:
      name: controller-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    driver: nfs
    fsType: nfs
    nodePublishSecretRef:
      name: node-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    nodeStageSecretRef:
      name: node-stage-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    volumeAttributes:
      node_attach_driver: nfs
      provisioner_driver: freenas-api-nfs
      server: 10.0.0.20
      share: /mnt/it-nas-6tb/k8s/volumes/pvc-bb231d3c-a425-46aa-8358-170b4de77709
      storage.kubernetes.io/csiProvisionerIdentity: 1698514144766-2257-nfs
    volumeHandle: pvc-bb231d3c-a425-46aa-8358-170b4de77709
  mountOptions:
  - noatime
  - nfsvers=4
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs-csi
  volumeMode: Filesystem
status:
  phase: Bound
```

- recipes-pvc

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"PersistentVolume","metadata":{"annotations":{"pv.kubernetes.io/provisioned-by":"nfs","volume.kubernetes.io/provisioner-deletion-secret-name":"provisioner-secret-nfs-csi-nfs-democratic-csi","volume.kubernetes.io/provisioner-deletion-secret-namespace":"democratic-csi"},"creationTimestamp":"2024-01-13T10:57:43Z","finalizers":["kubernetes.io/pv-protection"],"name":"pvc-95ca450d-fefd-4d5f-95f2-c4d7a084e033","resourceVersion":"38081721","uid":"5450dc06-983f-41f8-ab70-a23974ee23b0"},"spec":{"accessModes":["ReadWriteOnce"],"capacity":{"storage":"10Gi"},"csi":{"controllerExpandSecretRef":{"name":"controller-expand-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"controllerPublishSecretRef":{"name":"controller-publish-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"driver":"nfs","fsType":"nfs","nodePublishSecretRef":{"name":"node-publish-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"nodeStageSecretRef":{"name":"node-stage-secret-nfs-csi-nfs-democratic-csi","namespace":"democratic-csi"},"volumeAttributes":{"node_attach_driver":"nfs","provisioner_driver":"freenas-api-nfs","server":"10.0.0.20","share":"/mnt/it-nas-6tb/k8s/volumes/pvc-95ca450d-fefd-4d5f-95f2-c4d7a084e033","storage.kubernetes.io/csiProvisionerIdentity":"1704586955554-5837-nfs"},"volumeHandle":"pvc-95ca450d-fefd-4d5f-95f2-c4d7a084e033"},"mountOptions":["noatime","nfsvers=4"],"persistentVolumeReclaimPolicy":"Retain","storageClassName":"nfs-csi","volumeMode":"Filesystem"},"status":{"phase":"Available"}}
    pv.kubernetes.io/bound-by-controller: "yes"
    pv.kubernetes.io/provisioned-by: nfs
    volume.kubernetes.io/provisioner-deletion-secret-name: provisioner-secret-nfs-csi-nfs-democratic-csi
    volume.kubernetes.io/provisioner-deletion-secret-namespace: democratic-csi
  creationTimestamp: "2024-04-01T23:53:58Z"
  finalizers:
  - kubernetes.io/pv-protection
  name: pvc-95ca450d-fefd-4d5f-95f2-c4d7a084e033
  resourceVersion: "38082085"
  uid: 3e6ca748-28ca-4e90-89f8-6df41d24db9e
spec:
  accessModes:
  - ReadWriteOnce
  capacity:
    storage: 10Gi
  claimRef:
    apiVersion: v1
    kind: PersistentVolumeClaim
    name: recipes-pvc
    namespace: recipes
    resourceVersion: "38082083"
    uid: ba43a8f7-ab4a-4a16-ad18-d091e25f8ac4
  csi:
    controllerExpandSecretRef:
      name: controller-expand-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    controllerPublishSecretRef:
      name: controller-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    driver: nfs
    fsType: nfs
    nodePublishSecretRef:
      name: node-publish-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    nodeStageSecretRef:
      name: node-stage-secret-nfs-csi-nfs-democratic-csi
      namespace: democratic-csi
    volumeAttributes:
      node_attach_driver: nfs
      provisioner_driver: freenas-api-nfs
      server: 10.0.0.20
      share: /mnt/it-nas-6tb/k8s/volumes/pvc-95ca450d-fefd-4d5f-95f2-c4d7a084e033
      storage.kubernetes.io/csiProvisionerIdentity: 1704586955554-5837-nfs
    volumeHandle: pvc-95ca450d-fefd-4d5f-95f2-c4d7a084e033
  mountOptions:
  - noatime
  - nfsvers=4
  persistentVolumeReclaimPolicy: Retain
  storageClassName: nfs-csi
  volumeMode: Filesystem
status:
  phase: Bound
```

- Ingress NGINX deployment

```yaml
apiVersion: v1
items:
- apiVersion: apps/v1
  kind: Deployment
  metadata:
    annotations:
      deployment.kubernetes.io/revision: "2"
      kubectl.kubernetes.io/last-applied-configuration: |
        {"apiVersion":"apps/v1","kind":"Deployment","metadata":{"annotations":{},"labels":{"app.kubernetes.io/component":"controller","app.kubernetes.io/instance":"ingress-nginx","app.kubernetes.io/name":"ingress-nginx","app.kubernetes.io/part-of":"ingress-nginx","app.kubernetes.io/version":"1.9.4"},"name":"ingress-nginx-controller","namespace":"ingress-nginx"},"spec":{"minReadySeconds":0,"revisionHistoryLimit":10,"selector":{"matchLabels":{"app.kubernetes.io/component":"controller","app.kubernetes.io/instance":"ingress-nginx","app.kubernetes.io/name":"ingress-nginx"}},"strategy":{"rollingUpdate":{"maxUnavailable":1},"type":"RollingUpdate"},"template":{"metadata":{"labels":{"app.kubernetes.io/component":"controller","app.kubernetes.io/instance":"ingress-nginx","app.kubernetes.io/name":"ingress-nginx","app.kubernetes.io/part-of":"ingress-nginx","app.kubernetes.io/version":"1.9.4"}},"spec":{"containers":[{"args":["/nginx-ingress-controller","--publish-service=$(POD_NAMESPACE)/ingress-nginx-controller","--election-id=ingress-nginx-leader","--controller-class=k8s.io/ingress-nginx","--ingress-class=nginx","--configmap=$(POD_NAMESPACE)/ingress-nginx-controller","--validating-webhook=:8443","--validating-webhook-certificate=/usr/local/certificates/cert","--validating-webhook-key=/usr/local/certificates/key"],"env":[{"name":"POD_NAME","valueFrom":{"fieldRef":{"fieldPath":"metadata.name"}}},{"name":"POD_NAMESPACE","valueFrom":{"fieldRef":{"fieldPath":"metadata.namespace"}}},{"name":"LD_PRELOAD","value":"/usr/local/lib/libmimalloc.so"}],"image":"registry.k8s.io/ingress-nginx/controller:v1.9.4@sha256:5b161f051d017e55d358435f295f5e9a297e66158f136321d9b04520ec6c48a3","imagePullPolicy":"IfNotPresent","lifecycle":{"preStop":{"exec":{"command":["/wait-shutdown"]}}},"livenessProbe":{"failureThreshold":5,"httpGet":{"path":"/healthz","port":10254,"scheme":"HTTP"},"initialDelaySeconds":10,"periodSeconds":10,"successThreshold":1,"timeoutSeconds":1},"name":"controller","ports":[{"containerPort":80,"name":"http","protocol":"TCP"},{"containerPort":443,"name":"https","protocol":"TCP"},{"containerPort":8443,"name":"webhook","protocol":"TCP"}],"readinessProbe":{"failureThreshold":3,"httpGet":{"path":"/healthz","port":10254,"scheme":"HTTP"},"initialDelaySeconds":10,"periodSeconds":10,"successThreshold":1,"timeoutSeconds":1},"resources":{"requests":{"cpu":"100m","memory":"90Mi"}},"securityContext":{"allowPrivilegeEscalation":true,"capabilities":{"add":["NET_BIND_SERVICE"],"drop":["ALL"]},"runAsUser":101},"volumeMounts":[{"mountPath":"/usr/local/certificates/","name":"webhook-cert","readOnly":true}]}],"dnsPolicy":"ClusterFirst","nodeSelector":{"kubernetes.io/os":"linux"},"serviceAccountName":"ingress-nginx","terminationGracePeriodSeconds":300,"volumes":[{"name":"webhook-cert","secret":{"secretName":"ingress-nginx-admission"}}]}}}}
    creationTimestamp: "2023-10-28T16:12:22Z"
    generation: 2
    labels:
      app.kubernetes.io/component: controller
      app.kubernetes.io/instance: ingress-nginx
      app.kubernetes.io/name: ingress-nginx
      app.kubernetes.io/part-of: ingress-nginx
      app.kubernetes.io/version: 1.9.4
    name: ingress-nginx-controller
    namespace: ingress-nginx
    resourceVersion: "76075439"
    uid: baa8c961-1a6c-45b1-9fbd-16a7fff145a9
  spec:
    progressDeadlineSeconds: 600
    replicas: 1
    revisionHistoryLimit: 10
    selector:
      matchLabels:
        app.kubernetes.io/component: controller
        app.kubernetes.io/instance: ingress-nginx
        app.kubernetes.io/name: ingress-nginx
    strategy:
      rollingUpdate:
        maxSurge: 25%
        maxUnavailable: 1
      type: RollingUpdate
    template:
      metadata:
        annotations:
          container.apparmor.security.beta.kubernetes.io/controller: localhost/kubearmor-ingress-nginx-ingress-nginx-controller-controller
          kubearmor-policy: enabled
        creationTimestamp: null
        labels:
          app.kubernetes.io/component: controller
          app.kubernetes.io/instance: ingress-nginx
          app.kubernetes.io/name: ingress-nginx
          app.kubernetes.io/part-of: ingress-nginx
          app.kubernetes.io/version: 1.9.4
      spec:
        containers:
        - args:
          - /nginx-ingress-controller
          - --publish-service=$(POD_NAMESPACE)/ingress-nginx-controller
          - --election-id=ingress-nginx-leader
          - --controller-class=k8s.io/ingress-nginx
          - --ingress-class=nginx
          - --configmap=$(POD_NAMESPACE)/ingress-nginx-controller
          - --validating-webhook=:8443
          - --validating-webhook-certificate=/usr/local/certificates/cert
          - --validating-webhook-key=/usr/local/certificates/key
          env:
          - name: POD_NAME
            valueFrom:
              fieldRef:
                apiVersion: v1
                fieldPath: metadata.name
          - name: POD_NAMESPACE
            valueFrom:
              fieldRef:
                apiVersion: v1
                fieldPath: metadata.namespace
          - name: LD_PRELOAD
            value: /usr/local/lib/libmimalloc.so
          image: registry.k8s.io/ingress-nginx/controller:v1.9.4@sha256:5b161f051d017e55d358435f295f5e9a297e66158f136321d9b04520ec6c48a3
          imagePullPolicy: IfNotPresent
          lifecycle:
            preStop:
              exec:
                command:
                - /wait-shutdown
          livenessProbe:
            failureThreshold: 5
            httpGet:
              path: /healthz
              port: 10254
              scheme: HTTP
            initialDelaySeconds: 10
            periodSeconds: 10
            successThreshold: 1
            timeoutSeconds: 1
          name: controller
          ports:
          - containerPort: 80
            name: http
            protocol: TCP
          - containerPort: 443
            name: https
            protocol: TCP
          - containerPort: 8443
            name: webhook
            protocol: TCP
          readinessProbe:
            failureThreshold: 3
            httpGet:
              path: /healthz
              port: 10254
              scheme: HTTP
            initialDelaySeconds: 10
            periodSeconds: 10
            successThreshold: 1
            timeoutSeconds: 1
          resources:
            requests:
              cpu: 100m
              memory: 90Mi
          securityContext:
            allowPrivilegeEscalation: true
            capabilities:
              add:
              - NET_BIND_SERVICE
              drop:
              - ALL
            runAsUser: 101
          terminationMessagePath: /dev/termination-log
          terminationMessagePolicy: File
          volumeMounts:
          - mountPath: /usr/local/certificates/
            name: webhook-cert
            readOnly: true
        dnsPolicy: ClusterFirst
        nodeSelector:
          kubernetes.io/os: linux
        restartPolicy: Always
        schedulerName: default-scheduler
        securityContext: {}
        serviceAccount: ingress-nginx
        serviceAccountName: ingress-nginx
        terminationGracePeriodSeconds: 300
        volumes:
        - name: webhook-cert
          secret:
            defaultMode: 420
            secretName: ingress-nginx-admission
  status:
    availableReplicas: 1
    conditions:
    - lastTransitionTime: "2023-10-28T16:12:22Z"
      lastUpdateTime: "2023-10-28T16:12:22Z"
      message: Deployment has minimum availability.
      reason: MinimumReplicasAvailable
      status: "True"
      type: Available
    - lastTransitionTime: "2023-10-28T16:12:22Z"
      lastUpdateTime: "2024-03-19T09:38:57Z"
      message: ReplicaSet "ingress-nginx-controller-6d9f476bcf" has successfully progressed.
      reason: NewReplicaSetAvailable
      status: "True"
      type: Progressing
    observedGeneration: 2
    readyReplicas: 1
    replicas: 1
    updatedReplicas: 1
kind: List
metadata:
  resourceVersion: ""
```

- Ingress NGINX service

```yaml
apiVersion: v1
items:
- apiVersion: v1
  kind: Service
  metadata:
    annotations:
      kubectl.kubernetes.io/last-applied-configuration: |
        {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"app.kubernetes.io/component":"controller","app.kubernetes.io/instance":"ingress-nginx","app.kubernetes.io/name":"ingress-nginx","app.kubernetes.io/part-of":"ingress-nginx","app.kubernetes.io/version":"1.9.4"},"name":"ingress-nginx-controller","namespace":"ingress-nginx"},"spec":{"externalTrafficPolicy":"Local","ipFamilies":["IPv4"],"ipFamilyPolicy":"SingleStack","ports":[{"appProtocol":"http","name":"http","port":80,"protocol":"TCP","targetPort":"http"},{"appProtocol":"https","name":"https","port":443,"protocol":"TCP","targetPort":"https"}],"selector":{"app.kubernetes.io/component":"controller","app.kubernetes.io/instance":"ingress-nginx","app.kubernetes.io/name":"ingress-nginx"},"type":"LoadBalancer"}}
      metallb.universe.tf/ip-allocated-from-pool: service-pool
    creationTimestamp: "2023-10-28T16:12:22Z"
    labels:
      app.kubernetes.io/component: controller
      app.kubernetes.io/instance: ingress-nginx
      app.kubernetes.io/name: ingress-nginx
      app.kubernetes.io/part-of: ingress-nginx
      app.kubernetes.io/version: 1.9.4
    name: ingress-nginx-controller
    namespace: ingress-nginx
    resourceVersion: "1080426"
    uid: 53dd3c08-142e-41bc-8a15-0cd6311ab14e
  spec:
    allocateLoadBalancerNodePorts: true
    clusterIP: 10.107.203.76
    clusterIPs:
    - 10.107.203.76
    externalTrafficPolicy: Local
    healthCheckNodePort: 31503
    internalTrafficPolicy: Cluster
    ipFamilies:
    - IPv4
    ipFamilyPolicy: SingleStack
    ports:
    - appProtocol: http
      name: http
      nodePort: 32514
      port: 80
      protocol: TCP
      targetPort: http
    - appProtocol: https
      name: https
      nodePort: 32317
      port: 443
      protocol: TCP
      targetPort: https
    selector:
      app.kubernetes.io/component: controller
      app.kubernetes.io/instance: ingress-nginx
      app.kubernetes.io/name: ingress-nginx
    sessionAffinity: None
    type: LoadBalancer
  status:
    loadBalancer:
      ingress:
      - ip: 10.0.0.100
- apiVersion: v1
  kind: Service
  metadata:
    annotations:
      kubectl.kubernetes.io/last-applied-configuration: |
        {"apiVersion":"v1","kind":"Service","metadata":{"annotations":{},"labels":{"app.kubernetes.io/component":"controller","app.kubernetes.io/instance":"ingress-nginx","app.kubernetes.io/name":"ingress-nginx","app.kubernetes.io/part-of":"ingress-nginx","app.kubernetes.io/version":"1.9.4"},"name":"ingress-nginx-controller-admission","namespace":"ingress-nginx"},"spec":{"ports":[{"appProtocol":"https","name":"https-webhook","port":443,"targetPort":"webhook"}],"selector":{"app.kubernetes.io/component":"controller","app.kubernetes.io/instance":"ingress-nginx","app.kubernetes.io/name":"ingress-nginx"},"type":"ClusterIP"}}
    creationTimestamp: "2023-10-28T16:12:22Z"
    labels:
      app.kubernetes.io/component: controller
      app.kubernetes.io/instance: ingress-nginx
      app.kubernetes.io/name: ingress-nginx
      app.kubernetes.io/part-of: ingress-nginx
      app.kubernetes.io/version: 1.9.4
    name: ingress-nginx-controller-admission
    namespace: ingress-nginx
    resourceVersion: "1080429"
    uid: 5f6d8b65-5268-418d-8ea4-152ae1820886
  spec:
    clusterIP: 10.108.151.248
    clusterIPs:
    - 10.108.151.248
    internalTrafficPolicy: Cluster
    ipFamilies:
    - IPv4
    ipFamilyPolicy: SingleStack
    ports:
    - appProtocol: https
      name: https-webhook
      port: 443
      protocol: TCP
      targetPort: webhook
    selector:
      app.kubernetes.io/component: controller
      app.kubernetes.io/instance: ingress-nginx
      app.kubernetes.io/name: ingress-nginx
    sessionAffinity: None
    type: ClusterIP
  status:
    loadBalancer: {}
kind: List
metadata:
  resourceVersion: ""
```