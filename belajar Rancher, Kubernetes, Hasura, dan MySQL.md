# RANCHER (KUBERNETES)
**Rancher** adalah platform manajemen Kubernetes yang mempermudah pengelolaan banyak kluster Kubernetes di berbagai lingkungan (cloud, on-premise, hybrid). Berikut adalah komponen utamanya:

![image](https://github.com/user-attachments/assets/f4b266e8-892a-4bab-beb7-ce79f839587e)

**1.Rancher Server:** Pusat kontrol untuk mengelola kluster dan pengguna.

**2.Cluster Management:** Mengelola dan memonitor beberapa kluster Kubernetes.

**3.Projects & Workloads:** Pengelompokan aplikasi di kluster menggunakan project.

**4.Catalog & Apps:** Instalasi aplikasi cepat melalui Helm Charts dan template.

**5.User Management & RBAC:** Autentikasi dan kontrol akses berbasis peran.

**6.Monitoring & Alerting:** Pemantauan kluster dengan Prometheus/Grafana dan notifikasi masalah.

  Rancher menyederhanakan manajemen Kubernetes, mendukung multi-cloud, dan menyediakan kontrol akses serta pemantauan yang kuat.
    Di dalam Rancher, Kubernetes adalah platform utama yang dikelola. Rancher mempermudah pengelolaan kluster Kubernetes dengan fitur:

  **Manajemen Kluster:** Membuat dan memantau banyak kluster dari satu tempat.

  **Otomatisasi Deploy:** Memudahkan deploy aplikasi tanpa perlu langsung ke CLI Kubernetes.

  **Namespace & Project:** Mengelola resources dengan lebih mudah menggunakan projects.
  
  **Policy:** Mengatur akses pengguna dengan kontrol RBAC.

  **Multi-Cluster:** Mengelola beberapa kluster sekaligus.

Rancher menyederhanakan penggunaan Kubernetes dengan antarmuka dan alat manajemen yang intuitif.

Pada kali ini saya akan menjelaskan bagaimana saya Deployment dan Service untuk **Hasura** yang terkoneksi dengan Rancher kubernetes

Pertama kita hasura membuat **deployment** nya terlebih dahulu

![image](https://github.com/user-attachments/assets/098ea80f-58ce-44b0-b5fa-ad9bf32bde21)
yang berisikan yaml berikut
```
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: '5'
  creationTimestamp: '2024-09-11T02:35:42Z'
  generation: 5
  labels:
    app: hasura-graphql-data-connector
    hasura-jeremiService: custom
    workload.user.cattle.io/workloadselector: apps.deployment-jeremi-hasura-jeremi
  managedFields:
    - apiVersion: apps/v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations: {}
          f:labels:
            .: {}
            f:app: {}
            f:hasura-jeremiService: {}
            f:workload.user.cattle.io/workloadselector: {}
        f:spec:
          f:progressDeadlineSeconds: {}
          f:replicas: {}
          f:revisionHistoryLimit: {}
          f:selector: {}
          f:strategy:
            f:rollingUpdate:
              .: {}
              f:maxSurge: {}
              f:maxUnavailable: {}
            f:type: {}
          f:template:
            f:metadata:
              f:labels:
                .: {}
                f:app: {}
                f:workload.user.cattle.io/workloadselector: {}
              f:namespace: {}
            f:spec:
              f:containers:
                k:{"name":"hasura-jeremi"}:
                  .: {}
                  f:env:
                    .: {}
                    k:{"name":"HASURA_GRAPHQL_ADMIN_SECRET"}:
                      .: {}
                      f:name: {}
                      f:value: {}
                    k:{"name":"HASURA_GRAPHQL_DATABASE_URL"}:
                      .: {}
                      f:name: {}
                      f:value: {}
                    k:{"name":"HASURA_GRAPHQL_DATABASE_URL_MYSQL"}:
                      .: {}
                      f:name: {}
                      f:value: {}
                    k:{"name":"HASURA_GRAPHQL_DEV_MODE"}:
                      .: {}
                      f:name: {}
                      f:value: {}
                    k:{"name":"HASURA_GRAPHQL_EE_LICENSE_KEY"}:
                      .: {}
                      f:name: {}
                      f:value: {}
                    k:{"name":"HASURA_GRAPHQL_ENABLE_CONSOLE"}:
                      .: {}
                      f:name: {}
                      f:value: {}
                    k:{"name":"HASURA_GRAPHQL_ENABLE_MULTIPLE_DATABASES"}:
                      .: {}
                      f:name: {}
                      f:value: {}
                  f:image: {}
                  f:imagePullPolicy: {}
                  f:name: {}
                  f:ports:
                    .: {}
                    k:{"containerPort":8080,"protocol":"TCP"}:
                      .: {}
                      f:containerPort: {}
                      f:name: {}
                      f:protocol: {}
                  f:resources: {}
                  f:securityContext:
                    .: {}
                    f:allowPrivilegeEscalation: {}
                    f:privileged: {}
                    f:readOnlyRootFilesystem: {}
                    f:runAsNonRoot: {}
                  f:terminationMessagePath: {}
                  f:terminationMessagePolicy: {}
              f:dnsPolicy: {}
              f:restartPolicy: {}
              f:schedulerName: {}
              f:securityContext: {}
              f:terminationGracePeriodSeconds: {}
      manager: agent
      operation: Update
      time: '2024-09-11T05:51:32Z'
    - apiVersion: apps/v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations:
            f:deployment.kubernetes.io/revision: {}
        f:status:
          f:availableReplicas: {}
          f:conditions:
            .: {}
            k:{"type":"Available"}:
              .: {}
              f:lastTransitionTime: {}
              f:lastUpdateTime: {}
              f:message: {}
              f:reason: {}
              f:status: {}
              f:type: {}
            k:{"type":"Progressing"}:
              .: {}
              f:lastTransitionTime: {}
              f:lastUpdateTime: {}
              f:message: {}
              f:reason: {}
              f:status: {}
              f:type: {}
          f:observedGeneration: {}
          f:readyReplicas: {}
          f:replicas: {}
          f:updatedReplicas: {}
      manager: kube-controller-manager
      operation: Update
      subresource: status
      time: '2024-09-11T07:04:19Z'
  name: hasura-jeremi
  namespace: jeremi
  resourceVersion: '14405489'
  uid: 56d67b46-438b-46b4-a448-a8ee0c6cffd8
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      workload.user.cattle.io/workloadselector: apps.deployment-jeremi-hasura-jeremi
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: hasura-graphql-data-connector
        workload.user.cattle.io/workloadselector: apps.deployment-jeremi-hasura-jeremi
      namespace: jeremi
    spec:
      containers:
        - env:
            - name: HASURA_GRAPHQL_DATABASE_URL
              value: postgres://jeremi:jeremi@10.100.13.205:5432/jeremi
            - name: HASURA_GRAPHQL_DATABASE_URL_MYSQL
              value: mysql://jeremi:jeremi@10.100.13.205:3306/jeremi
            - name: HASURA_GRAPHQL_ENABLE_MULTIPLE_DATABASES
              value: 'true'
            - name: HASURA_GRAPHQL_EE_LICENSE_KEY
              value: >-
                eyJhbGciOiJSUzI1NiIsImtpZCI6IjEiLCJ0eXAiOiJKV1QifQ.eyJpc3MiOiJIYXN1cmEiLCJzdWIiOiJpbmRyYUBhbGxkYXRhaW50LmNvbSIsImV4cCI6MTc0MzQ2NTYwMCwiaWF0IjoxNzExOTk3Mzg5LCJqdGkiOiIwNjdmNzJlNC1hOGIwLTQwZWQtOTE3Zi1jYzQ2NzVhNWYwOGIiLCJsaWNlbnNlX2V4cF9hdCI6MTc0MzQ2NTYwMCwiZ3JhY2VfZXhwX2F0IjoxNzQzNDY1NjAwLCJsaWNlbnNlX3R5cGUiOiJ0cmlhbCJ9.JYICPbZKpFrcpjMhN_2I-SPDUPRI39riScUq1GfBWWOuTPrDyx-2nw18drTH-vgxjbekrFGDf0BqywZT66f2ucq3um57e_1BTDAgTQs6uZ-Z6cAjs0AQmd7iuCQzworealzuNuxreh1vR_QJljupZZmdpn4Gw6vmIhh6nYzTgC-QMsxlnBpxLXkBywWLKaMGIuKBIV0QDFIvc8NCjWeM5Aff8NB6cj4Q8uXEhq4mcBLblBihUuIaVXB8kTYQmHlQjx7jxzTLWa1tc1fsofKqZgvJlLHFgRi_ErHkM3KLsGE61Ntw9j8IaKhLOXengSuLn47DXjuXxmqmqIvRFpS_XPUG3pOQ-Cw86UrQ4KBGvt5EOlg842rfvVFjpT1uZ3njXzXn7CsY0AwT77LnWrCjeLyldtl-wPyDf1wChGDAHYscqgmeqx4FqbbrEjhdbBrRN84B9-cJ0eIHtiGp6_ayyl2aF3jQbVzwbd6FJci8Y9e1UH776mOoJqFfTLLx5fPu
            - name: HASURA_GRAPHQL_ADMIN_SECRET
              value: hasura-jeremi
            - name: HASURA_GRAPHQL_ENABLE_CONSOLE
              value: 'true'
            - name: HASURA_GRAPHQL_DEV_MODE
              value: 'true'
          image: hasura/graphql-engine:v2.42.0
          imagePullPolicy: IfNotPresent
          name: hasura-jeremi
          ports:
            - containerPort: 8080
              name: http
              protocol: TCP
          resources: {}
          securityContext:
            allowPrivilegeEscalation: false
            privileged: false
            readOnlyRootFilesystem: false
            runAsNonRoot: false
          terminationMessagePath: /dev/termination-log
          terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 1
  conditions:
    - lastTransitionTime: '2024-09-11T02:35:42Z'
      lastUpdateTime: '2024-09-11T05:54:22Z'
      message: ReplicaSet "hasura-jeremi-754d57b656" has successfully progressed.
      reason: NewReplicaSetAvailable
      status: 'True'
      type: Progressing
    - lastTransitionTime: '2024-09-11T07:04:19Z'
      lastUpdateTime: '2024-09-11T07:04:19Z'
      message: Deployment has minimum availability.
      reason: MinimumReplicasAvailable
      status: 'True'
      type: Available
  observedGeneration: 5
  readyReplicas: 1
  replicas: 1
  updatedReplicas: 1

```

Setelah kita sudah membuat deployment lanjut ke pembuatan **service** nya dengan yaml sebagai berikut

```
apiVersion: v1
kind: Service
metadata:
  annotations:
    field.cattle.io/publicEndpoints: >-
      [{"addresses":["10.100.14.5"],"port":8084,"protocol":"TCP","serviceName":"jeremi:hasura-jeremi","allNodes":false}]
    metallb.universe.tf/ip-allocated-from-pool: default-pool
  creationTimestamp: '2024-09-09T10:06:47Z'
  managedFields:
    - apiVersion: v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations:
            .: {}
            f:metallb.universe.tf/ip-allocated-from-pool: {}
        f:status:
          f:loadBalancer:
            f:ingress: {}
      manager: controller
      operation: Update
      subresource: status
      time: '2024-09-09T10:06:47Z'
    - apiVersion: v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations:
            f:field.cattle.io/publicEndpoints: {}
        f:spec:
          f:allocateLoadBalancerNodePorts: {}
          f:externalTrafficPolicy: {}
          f:internalTrafficPolicy: {}
          f:ports:
            .: {}
            k:{"port":8084,"protocol":"TCP"}:
              .: {}
              f:name: {}
              f:port: {}
              f:protocol: {}
              f:targetPort: {}
          f:selector: {}
          f:sessionAffinity: {}
          f:type: {}
      manager: agent
      operation: Update
      time: '2024-09-11T05:53:47Z'
  name: hasura-jeremi
  namespace: jeremi
  resourceVersion: '14393680'
  uid: 51b4b0ed-21ab-4723-8402-f29206ddd5ed
spec:
  allocateLoadBalancerNodePorts: true
  clusterIP: 10.111.172.176
  clusterIPs:
    - 10.111.172.176
  externalTrafficPolicy: Cluster
  internalTrafficPolicy: Cluster
  ipFamilies:
    - IPv4
  ipFamilyPolicy: SingleStack
  ports:
    - name: hasura-jeremi
      nodePort: 31207
      port: 8084
      protocol: TCP
      targetPort: 8080
  selector:
    app: hasura-graphql-data-connector
  sessionAffinity: None
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
      - ip: 10.100.14.5
```

![image](https://github.com/user-attachments/assets/7aa9c424-2ac1-450a-972a-714196c45dac)
Berikut service yang telah berjalan 
Setelah sudah membuat **Deployment dan Service** langsung Kita jalankan Hasura sebagai berikut
`http://10.100.14.5:8084/`

![image](https://github.com/user-attachments/assets/5da94274-40ea-4f22-9c95-fb914d9f904d)
Disini Kita sudah terhubung dengan hasura dan langsung saja kita membuat Password dari hasura tersebut

![image](https://github.com/user-attachments/assets/fe1728ee-e91f-4254-8cf0-9e6eec27644b)

Kemudian kita akan langsung mengkoneksikan Mysql di Hasura nya, sebelum kita mengkoneksikan terlebih dahulu kita membuat 1 namespace default yang berada di rancher tersebut
sebagai berikut

![image](https://github.com/user-attachments/assets/c65b9c5c-402f-4e06-9286-41e204e0c8e4)
Berikut adalah gambaran bahwa kita telah membuat Deployment `hasura-graphql-data-connector` 

`Deployment hasura-graphql-data-connector.yaml`
```
apiVersion: apps/v1
kind: Deployment
metadata:
  annotations:
    deployment.kubernetes.io/revision: '1'
    field.cattle.io/publicEndpoints: >-
      [{"addresses":["10.100.14.9"],"port":8991,"protocol":"TCP","serviceName":"default:hasura-graphql-data-connector","allNodes":false},{"nodeName":":k8s-worker02.alldataint.local","addresses":["10.100.13.177"],"port":8081,"protocol":"TCP","podName":"default:hasura-graphql-data-connector-7f6bf5f9cb-kj47s","allNodes":false}]
  creationTimestamp: '2024-09-11T07:23:00Z'
  generation: 3
  labels:
    app: hasura-graphql-data-connector
  managedFields:
    - apiVersion: apps/v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations:
            f:field.cattle.io/publicEndpoints: {}
          f:labels:
            .: {}
            f:app: {}
        f:spec:
          f:progressDeadlineSeconds: {}
          f:replicas: {}
          f:revisionHistoryLimit: {}
          f:selector: {}
          f:strategy:
            f:rollingUpdate:
              .: {}
              f:maxSurge: {}
              f:maxUnavailable: {}
            f:type: {}
          f:template:
            f:metadata:
              f:labels:
                .: {}
                f:app: {}
            f:spec:
              f:containers:
                k:{"name":"hasura-graphql-data-connector"}:
                  .: {}
                  f:image: {}
                  f:imagePullPolicy: {}
                  f:name: {}
                  f:ports:
                    .: {}
                    k:{"containerPort":8081,"protocol":"TCP"}:
                      .: {}
                      f:containerPort: {}
                      f:hostPort: {}
                      f:protocol: {}
                  f:resources:
                    .: {}
                    f:limits:
                      .: {}
                      f:cpu: {}
                      f:memory: {}
                    f:requests:
                      .: {}
                      f:cpu: {}
                      f:memory: {}
                  f:terminationMessagePath: {}
                  f:terminationMessagePolicy: {}
              f:dnsPolicy: {}
              f:restartPolicy: {}
              f:schedulerName: {}
              f:securityContext: {}
              f:terminationGracePeriodSeconds: {}
      manager: agent
      operation: Update
      time: '2024-09-11T07:37:21Z'
    - apiVersion: apps/v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations:
            .: {}
            f:deployment.kubernetes.io/revision: {}
        f:status:
          f:availableReplicas: {}
          f:conditions:
            .: {}
            k:{"type":"Available"}:
              .: {}
              f:lastTransitionTime: {}
              f:lastUpdateTime: {}
              f:message: {}
              f:reason: {}
              f:status: {}
              f:type: {}
            k:{"type":"Progressing"}:
              .: {}
              f:lastTransitionTime: {}
              f:lastUpdateTime: {}
              f:message: {}
              f:reason: {}
              f:status: {}
              f:type: {}
          f:observedGeneration: {}
          f:readyReplicas: {}
          f:replicas: {}
          f:updatedReplicas: {}
      manager: kube-controller-manager
      operation: Update
      subresource: status
      time: '2024-09-11T07:37:21Z'
  name: hasura-graphql-data-connector
  namespace: default
  resourceVersion: '14411152'
  uid: fc0ee2bb-6550-4c83-bbcf-967d427a750a
spec:
  progressDeadlineSeconds: 600
  replicas: 1
  revisionHistoryLimit: 10
  selector:
    matchLabels:
      app: hasura-graphql-data-connector
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      creationTimestamp: null
      labels:
        app: hasura-graphql-data-connector
    spec:
      containers:
        - image: hasura/graphql-data-connector:v2.43.0
          imagePullPolicy: IfNotPresent
          name: hasura-graphql-data-connector
          ports:
            - containerPort: 8081
              hostPort: 8081
              protocol: TCP
          resources:
            limits:
              cpu: 500m
              memory: 512Mi
            requests:
              cpu: 250m
              memory: 256Mi
          terminationMessagePath: /dev/termination-log
          terminationMessagePolicy: File
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      schedulerName: default-scheduler
      securityContext: {}
      terminationGracePeriodSeconds: 30
status:
  availableReplicas: 1
  conditions:
    - lastTransitionTime: '2024-09-11T07:33:53Z'
      lastUpdateTime: '2024-09-11T07:33:53Z'
      message: Deployment has minimum availability.
      reason: MinimumReplicasAvailable
      status: 'True'
      type: Available
    - lastTransitionTime: '2024-09-11T07:33:53Z'
      lastUpdateTime: '2024-09-11T07:33:53Z'
      message: >-
        ReplicaSet "hasura-graphql-data-connector-7f6bf5f9cb" has successfully
        progressed.
      reason: NewReplicaSetAvailable
      status: 'True'
      type: Progressing
  observedGeneration: 3
  readyReplicas: 1
  replicas: 1
  updatedReplicas: 1

```
Setelah itu kita membuat service nya juga sebagai berikut

`Service hasura-graphql-data-connector.yaml`
```
apiVersion: v1
kind: Service
metadata:
  annotations:
    field.cattle.io/publicEndpoints: >-
      [{"addresses":["10.100.14.9"],"port":8991,"protocol":"TCP","serviceName":"default:hasura-graphql-data-connector","allNodes":false}]
    metallb.universe.tf/ip-allocated-from-pool: default-pool
  creationTimestamp: '2024-09-11T07:37:21Z'
  managedFields:
    - apiVersion: v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations:
            f:field.cattle.io/publicEndpoints: {}
        f:spec:
          f:allocateLoadBalancerNodePorts: {}
          f:externalTrafficPolicy: {}
          f:internalTrafficPolicy: {}
          f:ports:
            .: {}
            k:{"port":8991,"protocol":"TCP"}:
              .: {}
              f:port: {}
              f:protocol: {}
              f:targetPort: {}
          f:selector: {}
          f:sessionAffinity: {}
          f:type: {}
      manager: agent
      operation: Update
      time: '2024-09-11T07:37:21Z'
    - apiVersion: v1
      fieldsType: FieldsV1
      fieldsV1:
        f:metadata:
          f:annotations:
            .: {}
            f:metallb.universe.tf/ip-allocated-from-pool: {}
        f:status:
          f:loadBalancer:
            f:ingress: {}
      manager: controller
      operation: Update
      subresource: status
      time: '2024-09-11T07:37:21Z'
  name: hasura-graphql-data-connector
  namespace: default
  resourceVersion: '14411148'
  uid: bccf8148-5318-4a28-9089-7103ee88f063
spec:
  allocateLoadBalancerNodePorts: true
  clusterIP: 10.110.92.67
  clusterIPs:
    - 10.110.92.67
  externalTrafficPolicy: Cluster
  internalTrafficPolicy: Cluster
  ipFamilies:
    - IPv4
  ipFamilyPolicy: SingleStack
  ports:
    - nodePort: 31569
      port: 8991
      protocol: TCP
      targetPort: 8081
  selector:
    app: hasura-graphql-data-connector
  sessionAffinity: None
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
      - ip: 10.100.14.9

```

![image](https://github.com/user-attachments/assets/1fd3fa05-bcc5-4aeb-a6bc-4b24295d2c38)



