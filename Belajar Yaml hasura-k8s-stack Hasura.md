# .gitignore
```
secret.prod.yaml
```
secret.prod.yaml dalam file .gitignore berarti Git mengabaikan file tersebut dan tidak melacak atau menyimpan perubahan pada file tersebut di repositori. Ini biasanya dilakukan untuk file yang berisi informasi sensitif, seperti kunci API, kata sandi, atau konfigurasi produksi, agar tidak secara tidak sengaja dipublikasikan atau dibagikan.

# config.yaml
```
endpoint: http://localhost:8080
```
`config.yaml` dengan endpoint: `http://localhost:8080` berarti aplikasi untuk mengakses layanan atau API yang berjalan di komputer lokal (localhost) pada port 8080. Alamat ini digunakan agar aplikasi bisa berkomunikasi dengan layanan tersebut. Port 8080 digunakan karena sering tersedia sebagai alternatif default untuk server web,menghindari konflik dengan port 80 yang biasanya sudah dipakai, dan tidak memerlukan izin administratif.terutama jika port 80 (port default untuk HTTP)

# deployment-service.yaml
## 1. Deployment
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: hasura
spec:
  selector:
    matchLabels:
      app: hasura
  template:
    metadata:
      labels:
        app: hasura
    spec:
      containers:
      - name: hasura
        image: hasura/graphql-engine:v1.0.0-alpha39
        env:
        - name: HASURA_GRAPHQL_DATABASE_URL
          valueFrom:
            secretKeyRef:
              key: dburl
              name: hasura
        - name: HASURA_GRAPHQL_ACCESS_KEY
          valueFrom:
           secretKeyRef:
             key: accessKey
             name: hasura
        - name: HASURA_GRAPHQL_ENABLE_CONSOLE
          value: "true"
        resources:
          limits:
            memory: "256Mi"
            cpu: "500m"
          requests:
            memory: "128Mi"
            cpu: "50m"
        ports:
        - containerPort: 8080

```
File hasura `deployment-service.yaml` yang berisi dua bagian: sebuah `Deployment` untuk menjalankan Hasura GraphQL Engine dan sebuah `Service` untuk mengaksesnya. Berikut adalah penjelasan dari masing-masing bagian:

Penjelasan:
* **apiVersion: apps/v1:** Versi API Kubernetes yang digunakan untuk mendefinisikan Deployment.
* **kind: Deployment:** Menunjukkan bahwa ini adalah objek Deployment.
* **metadata:** Mengandung metadata seperti name, yang menetapkan nama Deployment ini sebagai "hasura".
* **spec:**
  * **selector:** Menentukan pod mana yang akan dikelola oleh Deployment ini dengan mencocokkan label app: hasura.
  * **template:** Ini adalah template yang digunakan untuk membuat pod-pod.
    * **metadata:** Berisi label yang akan diterapkan pada setiap pod yang dibuat.
    * **spec:**
        * **containers:** Daftar container yang akan dijalankan di setiap pod.
          * **name: hasura:** Nama container.
            * **image:** hasura/graphql-engine .0.0-alpha39: Gambar Docker yang digunakan untuk container ini.
            * **env:** Variabel lingkungan yang akan disetel untuk container ini.
              * **HASURA_GRAPHQL_DATABASE_URL:** URL database yang akan digunakan oleh Hasura, diambil dari secret.
              * **HASURA_GRAPHQL_ACCESS_KEY:** Kunci akses untuk Hasura, juga diambil dari secret.
              * **HASURA_GRAPHQL_ENABLE_CONSOLE:** Mengaktifkan konsol Hasura dengan nilai "true".
            * **resources:**
              * **limits:** Batasan sumber daya yang diizinkan untuk container ini, yaitu 256MiB untuk memori dan 500m (0.5 CPU).
              * **requests:** Permintaan minimum sumber daya untuk container ini, yaitu 128MiB untuk memori dan 50m (0.05 CPU).
            * **ports:** Menentukan bahwa container ini akan mendengarkan pada port 8080.

## 2. Service
```
apiVersion: v1
kind: Service
metadata:
  name: hasura
spec:
  selector:
    app: hasura
  ports:
  - port: 80
    targetPort: 8080

```
**Penjelasan:**

* **apiVersion:** v1: Versi API Kubernetes yang digunakan untuk mendefinisikan `Service`.
* **kind:** Service: Menunjukkan bahwa ini adalah objek `Service`.
* **metadata:** Mengandung metadata seperti name, yang menetapkan `nama` Service ini sebagai "hasura".
* **spec:**
  * **selector:** Menentukan pod mana yang akan dipilih oleh `Service` ini, berdasarkan label `app: hasura`.
  * **ports:** Mendefinisikan aturan port untuk `Service` ini.
    * **port: 80:** `Service` ini akan mendengarkan pada port 80.
    * **targetPort: 8080:** Traffic yang diterima pada port 80 akan diteruskan ke port 8080 pada container.
      
Secara keseluruhan, file ini mengonfigurasi Kubernetes untuk menjalankan Hasura GraphQL Engine dalam sebuah pod, kemudian mengeksposnya melalui sebuah Service yang mendengarkan pada port 80.

# ingress.yaml
```
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: hasura
  annotations:
    kubernetes.io/ingress.class: "nginx"    
    certmanager.k8s.io/issuer: "letsencrypt-staging"
    #certmanager.k8s.io/issuer: "letsencrypt-prod"
    certmanager.k8s.io/acme-challenge-type: http01

spec:
  tls:
  - hosts:
    - k8s-stack.hasura.app
    secretName: k8s-stack-hasura-app-tls
  rules:
  - host: k8s-stack.hasura.app
    http:
      paths:
      - path: /
        backend:
          serviceName: hasura
          servicePort: 80
```
`ingress.yaml` adalah file konfigurasi untuk mengatur akses ke aplikasi di dalam klaster Kubernetes.

Penjelasan:
* **apiVersion:** Ini menentukan versi API Kubernetes yang digunakan. Di sini, `extensions/v1beta1` adalah versi lama untuk Ingress. Versi terbaru `networking.k8s.io/v1`
* **kind:** Menyatakan jenis objek Kubernetes yang sedang didefinisikan, yaitu `Ingress`.
* **metadata:**
  * **name:** Nama dari objek Ingress, yaitu `hasura`.
  * **annotations:** Metadata tambahan untuk konfigurasi khusus:
    * **`kubernetes.io/ingress.class`:** Menentukan kelas Ingress yang digunakan, di sini "nginx".
    * **`certmanager.k8s.io/issuer`:** Menunjukkan issuer sertifikat untuk TLS. Di sini menggunakan "letsencrypt-staging" untuk sertifikat dari Let’s Encrypt dalam mode staging (uji                                            coba). bisa mengganti ke "letsencrypt-prod" untuk produksi.
    * **`certmanager.k8s.io/acme-challenge-type`:** Tipe tantangan ACME yang digunakan untuk validasi sertifikat, yaitu `http01`.

* **spec:**
  * **tls:** Bagian ini mengonfigurasi TLS (Transport Layer Security) untuk mengamankan komunikasi:
    * **hosts:** Daftar nama host yang akan menggunakan TLS, di sini `k8s-stack.hasura.app`.
    * **secretName:** Nama dari secret yang berisi sertifikat TLS dan kunci privatnya, yaitu `k8s-stack-hasura-app-tls`.
* **rules:** Mengatur aturan untuk rute jaringan HTTP:
  * **host:** Nama host yang harus dicocokkan untuk aturan ini, yaitu `k8s-stack.hasura.app`.
  * **http:**
    * **paths:** Daftar jalur untuk menangani permintaan HTTP:
      * **path:** Jalur yang akan diteruskan, di sini `/` yang berarti semua permintaan untuk host ini akan diteruskan.
      * **backend:** Mengarahkan permintaan ke layanan backend:
        * **serviceName:** Nama layanan yang akan menangani permintaan, yaitu `hasura`.
        * **servicePort:** Port pada layanan yang dituju, yaitu port 80.
          
Secara keseluruhan, file ini mengatur Ingress untuk meneruskan lalu lintas dari `k8s-stack.hasura.app` ke layanan `hasura` di port 80 dan mengonfigurasi TLS untuk keamanan komunikasi.

# secret.yaml
```
apiVersion: v1
kind: Secret
metadata:
  name: hasura
stringData:
  accessKey: accessKey
  # only change postgres username, password and dbname as set
  # in postgres secret
  dburl: postgres://username:password@postgres:5432/dbname
```
File `secret.yaml` adalah sebuah file konfigurasi Kubernetes untuk mendefinisikan sebuah Secret. Secret dalam Kubernetes digunakan untuk menyimpan data sensitif seperti password, token, atau kunci SSH. Berikut adalah penjelasan untuk setiap bagian dari file secret.yaml tersebut:

* **`apiVersion: v1`** Menunjukkan versi API Kubernetes yang digunakan untuk objek ini. Versi v1 adalah versi stabil.
* **`kind: Secret`** Menyatakan bahwa jenis objek Kubernetes ini adalah Secret.
* **`metadata`** Bagian ini berisi metadata tentang objek Secret ini:
  * **name: hasura** Nama Secret ini adalah hasura. Nama ini digunakan untuk mengidentifikasi dan merujuk Secret di dalam cluster Kubernetes.
* **stringData** Bagian ini digunakan untuk mendefinisikan data sensitif sebagai string:
  * **accessKey: accessKey** Ini adalah contoh nilai kunci akses. Biasanya, akan mengganti accessKey dengan nilai kunci akses yang sebenarnya.
  * **dburl: postgres://username:password@postgres:5432/dbname** Ini adalah URL koneksi ke database PostgreSQL yang digunakan oleh aplikasi.                                                                      yang perlu mengganti username, password, dan dbname dengan nilai yang sesuai.

file ini mendefinisikan `Secret` yang berisi informasi penting seperti kunci akses dan URL database untuk digunakan oleh aplikasi di Kubernetes.

**Migrations** dalam GitHub biasanya merujuk pada perubahan skema basis data yang dilacak dan dikelola melalui sistem kontrol versi. Ini membantu dalam mengelola evolusi skema basis data secara bersamaan dengan kode aplikasi

**Perbedaan dalam .gitignore**
**Hasura:** Lebih fokus pada file konfigurasi dan metadata yang dihasilkan oleh Hasura.
**PostgreSQL:** Lebih fokus pada file dump, log, dan file terkait database lainnya.
