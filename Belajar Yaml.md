# Hasura-k8s-stack [postgres] 

## .gitignore

`.gitignore` adalah file yang digunakan dalam proyek Git untuk menentukan file atau direktori yang ingin diabaikan oleh Git, sehingga tidak akan dimasukkan ke dalam repository.

Jika ada baris berisi `secret.prod.yaml` di dalam `.gitignore`, itu berarti Git akan mengabaikan file `secret.prod.yaml`, sehingga file tersebut tidak akan ditambahkan, diubah, atau dihapus dalam commit. Ini biasanya dilakukan untuk mencegah informasi sensitif, seperti kredensial atau konfigurasi produksi, tidak secara tidak sengaja dibagikan ke publik atau tim yang lebih luas.

## deployment-service.yaml

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: postgres
spec:
  selector:
    matchLabels:
      app: postgres
  template:
    metadata:
      labels:
        app: postgres
    spec:
      containers:
      - name: postgres
        image: postgres:11.1
        env:
        - name: PGDATA
          value: /var/lib/postgresql/data/pgdata
        - name: POSTGRES_PASSWORD
          valueFrom:
            secretKeyRef:
              key: password
              name: postgres
        - name: POSTGRES_USER
          valueFrom:
            secretKeyRef:
              key: username
              name: postgres
        - name: POSTGRES_DB
          valueFrom:
            secretKeyRef:
              key: dbname
              name: postgres
        resources:
          limits:
            memory: "512Mi"
            cpu: "1"
          requests:
            memory: "256Mi"
            cpu: "100m"
        ports:
        - containerPort: 5432
        volumeMounts:
        - mountPath: /var/lib/postgresql/data
          name: data
      volumes:
      - name: data
        persistentVolumeClaim:
          claimName: postgres
---
apiVersion: v1
kind: Service
metadata:
  name: postgres
spec:
  selector:
    app: postgres
  ports:
  - port: 5432
    targetPort: 5432
```
YAML di atas adalah konfigurasi Kubernetes untuk mendefinisikan Deployment dan Service yang menjalankan PostgreSQL versi 11.1. Berikut penjelasan singkatnya:

### Deployment

* **kind: Deployment:** Mengatur Deployment yang akan mengelola dan menjalankan Pod PostgreSQL.
  
* **metadata.name:** postgres: Memberi nama "postgres" untuk Deployment ini.

* **selector:** Digunakan untuk mencocokkan labels yang ada di Pod yang akan dijalankan.
  
* **template:** Bagian ini mendefinisikan Pod yang akan dibuat.
  * **metadata.labels:** Memberi label `app: postgres` untuk Pod.
  * **spec:** Mengatur spesifikasi dari kontainer di dalam Pod.
    * **containers:** Daftar kontainer yang akan dijalankan di Pod ini. Dalam hal ini, hanya ada satu kontainer.
      * **name:** postgres: Nama kontainernya.
      * **image:** postgres:11.1: Menjalankan PostgreSQL versi 11.1 dari Docker image.
      * **env:** Variabel lingkungan yang diperlukan oleh PostgreSQL:
        * **PGDATA:** Menentukan direktori data PostgreSQL.
        * **POSTGRES_PASSWORD, POSTGRES_USER, POSTGRES_DB:** Variabel untuk mengatur kata sandi, nama pengguna, dan nama database dari PostgreSQL. Nilainya diambil                                                                 dari Secret Kubernetes.
          
      * **resources:** Mengatur batasan dan permintaan sumber daya CPU dan memori untuk kontainer.
        Terdapat dua komponen utama: limits dan requests.
        ## 1. Limits
        memory: "512Mi": Membatasi penggunaan memori maksimum oleh kontainer hingga 512 MiB (Mebibytes). Jika kontainer mencoba menggunakan lebih dari 512 MiB,                Kubernetes akan mencoba menghentikan kontainer tersebut.
        
        cpu: "1": Membatasi penggunaan CPU maksimum oleh kontainer hingga 1 core CPU. Jika kontainer mencoba menggunakan lebih dari 1 core CPU, Kubernetes akan                mengekang penggunaan CPU-nya.

        ## 2. Requests
        memory: "256Mi": Menetapkan permintaan minimum memori sebesar 256 MiB. Ini adalah jumlah memori yang dijamin tersedia untuk kontainer. Jika tidak ada memori           sebanyak ini, Pod mungkin tidak akan dijadwalkan hingga memori yang cukup tersedia.
        
        cpu: "100m": Menetapkan permintaan minimum CPU sebesar 100 millicores (0.1 core CPU). Ini adalah jumlah CPU yang dijamin tersedia untuk kontainer.

        Penjelasan Mengenai cpu 100m:
        1 core CPU = 1000 millicores
        100 millicores = 0.1 core CPU
        Ini berarti ketika Anda menetapkan cpu: "100m" pada kontainer, Anda meminta agar kontainer dijamin dapat menggunakan 10% dari satu core CPU.
        Dalam Kubernetes, CPU dialokasikan dalam satuan yang disebut millicores atau millicpu. Satu millicore setara dengan 1/1000 dari satu core CPU.

        * **Requests** adalah sumber daya yang akan disediakan oleh Kubernetes saat menjalankan kontainer.
        * **Limits** adalah batas keras yang tidak boleh dilampaui oleh kontainer selama beroperasi.
        
      * **ports:** Mengekspos port 5432 dari kontainer, yang merupakan port default PostgreSQL.
        Port 5432 biasanya digunakan oleh PostgreSQL,port ini yang akan digunakan untuk berkomunikasi dengan database PostgreSQL tersebut.
        
      * **volumeMounts:** Menyambungkan volume bernama `data` ke direktori `/var/lib/postgresql/data` di dalam kontainer.
        
* **volumes:** Menyambungkan PersistentVolumeClaim bernama `postgres` ke volume `data`, digunakan untuk penyimpanan data yang persisten.
  Volume `data` digunakan untuk menyimpan data secara persisten di dalam Pod.

  `PersistentVolumeClaim` adalah permintaan untuk penyimpanan yang persisten.

  `claimName: postgres` mengacu pada PVC dengan nama `postgres`, yang akan menyediakan dan mengelola penyimpanan untuk volume ini.

Dengan cara ini, `data` yang disimpan di volume data akan tetap ada meskipun Pod di-restart atau dipindahkan, asalkan PVC `postgres` tetap ada.
  
### Service

* **kind:** Service: Membuat Service untuk mengakses Pod PostgreSQL.
* **metadata.name:** postgres: Memberi nama "postgres" untuk Service ini.
* **spec:** Menentukan spesifikasi Service.
  * **selector:** Memilih Pod yang memiliki label `app: postgres` untuk di-expose melalui Service ini.
  * **ports:** Mengekspos port 5432 di dalam Service, yang akan diarahkan ke port 5432 dari Pod.
    
Secara keseluruhan, konfigurasi ini menjalankan database PostgreSQL di Kubernetes dengan penyimpanan data yang persisten dan eksposur port yang dapat diakses oleh aplikasi lain di dalam cluster Kubernetes.

## pvc.yaml
```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: postgres
spec:
  accessModes:
  - ReadWriteOnce
  storageClassName: default
  resources:
    requests:
      storage: 5Gi
```

Ini adalah konfigurasi Kubernetes untuk PersistentVolumeClaim (PVC). PVC digunakan untuk meminta penyimpanan berkelanjutan yang akan digunakan oleh pod di Kubernetes. Berikut adalah penjelasan dari setiap bagian:

* **`apiVersion`:** v1: Menyatakan versi API yang digunakan untuk objek ini.
* **`kind: PersistentVolumeClaim`:** Tipe objek Kubernetes yang mendeklarasikan permintaan untuk penyimpanan.
* **`metadata`:**
  * **`name: postgres`:** Nama dari PVC ini adalah "postgres".
* **`spec`:** Spesifikasi dari PVC.
  * **accessModes:**
    * **ReadWriteOnce:** Menyatakan bahwa volume dapat diakses untuk dibaca dan ditulis hanya oleh satu pod pada satu waktu.
  * **storageClassName:** default: Menyatakan kelas penyimpanan yang akan digunakan. Dalam hal ini, menggunakan kelas penyimpanan yang bernama "default".
    * **resources:**
      * **requests:**
        * **storage: 5Gi:** Permintaan penyimpanan sebesar 5 gigabyte.
          
Dengan konfigurasi ini, PVC meminta 5GB penyimpanan yang dapat dibaca dan ditulis oleh satu pod, menggunakan kelas penyimpanan "default".

## secret.yaml

File YAML yang diatas menunjukan definisi sebuah `Secret` di Kubernetes.`Secret` ini digunakan untuk menyimpan data sensitif seperti password, token, atau kunci. Berikut penjelasan setiap bagiannya:

* **`apiVersion: v1` :** Versi API yang digunakan untuk membuat Secret. Versi ini menyatakan bahwa ini adalah objek Secret versi 1.
* **`kind: Secret` :** Menunjukkan bahwa objek ini adalah sebuah Secret.
* **`metadata` :**
  * **`name: postgres` :** Nama dari Secret ini adalah postgres. Nama ini digunakan untuk merujuk ke Secret ini di dalam Kubernetes.
* **`stringData` :**
  * **`username: username` :** Menyimpan data sensitif dengan key `username` dan value `username`.
  * **`password: password` :** Menyimpan data sensitif dengan key `password` dan value `password`.
  * **`dbname: dbname` :** Menyimpan data sensitif dengan key `dbname` dan value `dbname`.
`stringData` adalah cara untuk mendefinisikan data sensitif dengan format string. Kubernetes secara otomatis akan mengenkripsi data ini saat disimpan di cluster.
`Secret` ini di dalam konfigurasi Pod atau Deployment untuk memberikan akses ke data sensitif seperti kredensial database.

Penjelasan tambahan Mengenai **Cluster**
**cluster** adalah kumpulan mesin (node) yang bekerja bersama untuk menjalankan aplikasi dan layanan. Cluster Kubernetes biasanya terdiri dari dua tipe node:

* **Master Node:** Node ini mengelola cluster dan bertanggung jawab untuk pengaturan dan koordinasi, seperti menjalankan kontrol plane yang mengelola status cluster dan menugaskan beban kerja ke node lainnya.

* **Worker Node:** Node ini menjalankan aplikasi yang dikemas dalam container. Mereka menjalankan pod (unit terkecil dalam Kubernetes yang bisa menjalankan satu atau beberapa container) dan mengelola container yang berada di dalamnya.

**Cluster Kubernetes memiliki beberapa komponen penting:**

  * **API Server:** Titik masuk utama untuk semua permintaan ke cluster.
  * **Scheduler:** Menentukan node mana yang akan menjalankan pod.
  * **Controller Manager:** Mengelola berbagai kontroler yang mengawasi keadaan sistem dan membuat perubahan jika diperlukan.
  * **etcd:** Penyimpanan konfigurasi cluster yang terdistribusi.
  * **Kubelet:** Agen yang berjalan di setiap node dan memastikan bahwa kontainer yang dijadwalkan oleh API Server berjalan dengan benar.
  * **Kube-Proxy:** Mengelola komunikasi jaringan di dalam cluster, seperti load balancing dan routing trafik ke layanan yang benar.

Berikut Gambar
```
                      +------------------+
                      |    Master Node   |
                      +------------------+
                              |
       +----------------------------------------------------+
       |                  Control Plane                       |
       |                                                      |
       |  +------------+  +------------------+  +-----------+ |
       |  | API Server |  |Controller Manager| | Scheduler |  |
       |  +------------+  +------------------+  +-----------+ |
       |                                                      |
       +----------------+-----------------------------------+
                              |
        +---------------------------------------------+
        |               Worker Nodes                 |
        |                                            |
        | +------------------+ +-------------------+ |
        | |      Node 1      | |       Node 2      | |
        | |                  | |                   | |
        | | +------------+   | | +------------+    | |
        | | |   Pod 1    |   | | |   Pod 2    |    | |
        | | |            |   | | |            |    | |
        | | +------------+   | | +------------+    | |
        | +------------------+ +-------------------+ |
        |                                            |
        +---------------------------------------------+
```
