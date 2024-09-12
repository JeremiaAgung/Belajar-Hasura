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

Pertama kita hasura membuat deployment nya terlebih dahulu
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
![image](https://github.com/user-attachments/assets/12630e13-78d8-4441-b8e6-85c949ab3c7a)

Berikut Deployments yang telah berjalan 





