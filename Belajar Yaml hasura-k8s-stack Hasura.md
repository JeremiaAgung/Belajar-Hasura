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
