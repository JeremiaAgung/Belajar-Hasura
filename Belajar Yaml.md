# Hasura-k8s-stack [postgres] 

### .gitignore

`.gitignore` adalah file yang digunakan dalam proyek Git untuk menentukan file atau direktori yang ingin diabaikan oleh Git, sehingga tidak akan dimasukkan ke dalam repository.

Jika ada baris berisi `secret.prod.yaml` di dalam `.gitignore`, itu berarti Git akan mengabaikan file `secret.prod.yaml`, sehingga file tersebut tidak akan ditambahkan, diubah, atau dihapus dalam commit. Ini biasanya dilakukan untuk mencegah informasi sensitif, seperti kredensial atau konfigurasi produksi, tidak secara tidak sengaja dibagikan ke publik atau tim yang lebih luas.

### deployment-service.yaml

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

## Deployment

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
      * **ports:** Mengekspos port 5432 dari kontainer, yang merupakan port default PostgreSQL.
      * **volumeMounts:** Menyambungkan volume bernama `data` ke direktori `/var/lib/postgresql/data` di dalam kontainer.
        
* **volumes:** Menyambungkan PersistentVolumeClaim bernama `postgres` ke volume `data`, digunakan untuk penyimpanan data yang persisten.
  
## Service

* **kind:** Service: Membuat Service untuk mengakses Pod PostgreSQL.
* **metadata.name:** postgres: Memberi nama "postgres" untuk Service ini.
* **spec:** Menentukan spesifikasi Service.
  * **selector:** Memilih Pod yang memiliki label `app: postgres` untuk di-expose melalui Service ini.
  * **ports:** Mengekspos port 5432 di dalam Service, yang akan diarahkan ke port 5432 dari Pod.
    
Secara keseluruhan, konfigurasi ini menjalankan database PostgreSQL di Kubernetes dengan penyimpanan data yang persisten dan eksposur port yang dapat diakses oleh aplikasi lain di dalam cluster Kubernetes.
