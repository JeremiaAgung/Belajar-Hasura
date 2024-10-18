# Hasura DDN 
**Arsitektur Hasura DDN**

**Hasura Data Delivery Network (DDN)** memperkenalkan konsep "supergraph" untuk mengatasi masalah fragmentasi data ini. Supergraph adalah kerangka kerja yang menggabungkan berbagai sumber data ke dalam satu API yang aman dan konsisten.

* **Hasura Runtime Engine:** proses mengedit dan membangun metadata (seperti skema API, pengaturan data, dan peraturan akses) dilakukan secara terpisah dari waktu API dijalankan untuk melayani permintaan pengguna. Hasura DDN mengoptimalkan cara API dimulai dan dijalankan, sehingga API bisa mulai dengan sangat cepat dan tetap tersedia tanpa gangguan meskipun ada perubahan atau pembaruan. 

* **Native Data Connector (NDC) Specification:** bahwa Hasura DDN tidak lagi membatasi pada sumber data yang disebut "native" (seperti PostgreSQL, MySQL, atau database yang secara langsung didukung oleh Hasura). Sebaliknya, Hasura kini mendukung koneksi ke berbagai jenis sumber data, baik itu database maupun API, menggunakan Connector yang dirancang untuk menyediakan query native, push-down capabilities, dan connection pooling,.

* **Supergraph:** Sebuah arsitektur yang menggabungkan beberapa data domain (subgraphs) menjadi satu grafik, memungkinkan skalabilitas dan modularitas pada aplikasi atau sistem yang kompleks.

* **Subgraphs:** Bagian dari supergraph yang menangani domain tertentu (misalnya, produk, pengguna, pesanan). Setiap subgraph memiliki schema GraphQL sendiri dan dapat dikelola secara terpisah.

* **Hasura Cloud:** Menyediakan lapisan cloud untuk API global dengan kinerja tinggi dan alat untuk mengelola proyek, subgraph, dan build.

* **DDN CLI:** Alat baris perintah yang mempermudah pengelolaan metadata, build, dan deployment API di cloud.

* **DDN Console:** Platform visual untuk onboarding cepat, pengujian, dan pemantauan, dengan fitur-fitur seperti API explorer dan dashboard kesehatan operasional.

* **Builds:** Setiap perubahan metadata menghasilkan build atomik yang dapat di-deploy langsung tanpa kesalahan, dengan versi kontrol otomatis.
  
## Core Concept Hasura V3

![image](https://github.com/user-attachments/assets/20852889-54d2-4e5f-8050-66e48159a12f)

Pada Gambar Diatas menampilkan arsitektur sistem yang menggunakan Hasura sebagai platform utama untuk menyatukan berbagai sumber data dan API. 
Berikut penjelasan elemen-elemen utama di dalamnya:

**Client Apps, Public APIs, Internal Apps**:
Ini menggambarkan tiga kategori aplikasi atau layanan yang memanfaatkan data dari Hasura.

* **Client Apps** dapat berupa aplikasi pengguna akhir seperti aplikasi web atau mobile.
* **Public APIs** adalah antarmuka yang dapat diakses oleh layanan eksternal untuk mengkonsumsi data dari sistem.
* **Internal Apps** adalah aplikasi internal perusahaan yang juga memanfaatkan data dari Hasura.
Ketiga elemen ini berinteraksi dengan Hasura, yang menyediakan data secara real-time melalui GraphQL API, baik untuk aplikasi publik, internal, atau eksternal.

**Supergraph & Hasura**:
* Supergraph merujuk pada federasi GraphQL atau layer yang menyatukan berbagai sumber data di bawah satu API GraphQL.
* Hasura berfungsi sebagai platform GraphQL yang mengelola akses ke berbagai sumber data dengan menyediakan API GraphQL real-time tanpa perlu banyak konfigurasi kode.

**Connector**:
* **Connectors** adalah penghubung antara Hasura dengan sumber data yang berbeda.
* Data API/Microservice merujuk pada mikroservis atau API yang menyediakan data yang dikonsumsi oleh Hasura.
* Data Source adalah database atau data warehouse tradisional.
* External Source adalah sumber data dari luar, yang bisa berupa layanan pihak ketiga atau sumber data eksternal lainnya.

Secara keseluruhan, diagram ini menunjukkan bagaimana Hasura digunakan untuk menyatukan berbagai sumber data melalui konektor dan menyajikannya melalui API GraphQL kepada berbagai aplikasi atau layanan yang membutuhkan data tersebut.

## Arsitektur Control Plane & Data Plane

![image](https://github.com/user-attachments/assets/819e505b-bd2a-43b3-9240-815966a2c1ea)

**Control Plane**
Dalam Hasura Data Delivery Network (DDN), Developer menggunakan Control Plane untuk membuat dan mengelola supergraph—API GraphQL yang unik dan independen, yang dihasilkan dari build proyek. Setiap build menghasilkan API yang dapat dipantau dan dianalisis performanya, dengan fitur observabilitas yang mencatat jejak dan metrik penggunaan API. Developer dapat berkolaborasi dengan tim lain, berbagi API dengan konsumen, dan menerapkan pratinjau build untuk menguji perubahan sebelum diterapkan secara permanen. 
* **Control plane: Membangun metadata proyek (seperti schema dan permissions) dan mengelolanya.**

**Data Plane**
Data plane Hasura v3 Engine adalah komponen yang memproses permintaan GraphQL secara efisien dan skalabel. Ini menggunakan runtime serverless, data plane Hasura tidak menyimpan konfigurasi atau data permintaan secara permanen. Data connector juga mengelola connection pool on-demand untuk efisiensi. Data plane dapat dideploy di berbagai wilayah untuk mengoptimalkan latency dengan Anycast IP, dan tersedia di GCP, AWS, Azure, serta self-hosted jika mendukung jaringan yang diperlukan.
* **Data plane: Menangani eksekusi query GraphQL terhadap database, menggunakan metadata yang disediakan oleh control plane.**

## Authentication 
**Using JWTs**

![image](https://github.com/user-attachments/assets/4a89c4dd-27ec-4497-a883-188c6fe9a535)

Pada gambar ini menjelaskan cara mengonfigurasi Hasura agar menggunakan JSON Web Token (JWT) untuk autentikasi. JWT ini diberikan oleh layanan autentikasi (seperti login) dan dikirimkan oleh klien ke Hasura melalui header permintaan.

Hasura akan memverifikasi dan membaca token tersebut untuk mengambil informasi penting, seperti:

Peran pengguna (x-hasura-role): Untuk menentukan apa yang bisa diakses pengguna.
ID pengguna (x-hasura-user-id): Untuk mengidentifikasi pengguna.
Dengan cara ini, Hasura dapat menentukan akses pengguna ke data berdasarkan informasi dalam JWT. untuk membantu mengonfigurasi integrasi antara Hasura dan penyedia autentikasi (seperti Auth0, AWS Cognito, Firebase, atau Clerk).

**Using a Webhook**

![image](https://github.com/user-attachments/assets/c3a2af89-6408-466d-a1a0-d4cf5992160e)

Pada Gambar ini  mode webhook untuk autentikasi, 
berikut langkah-langkah:

* **Membuat Layanan Webhook:** Layanan ini menerima permintaan HTTP dari Hasura dengan header autentikasi dan mengembalikan informasi sesi pengguna dalam respons JSON, seperti X-Hasura-User-Id, X-Hasura-Role, dan lainnya.

* **Mengonfigurasi Hasura:** Di Hasura Console, pilih metode autentikasi Webhook, lalu masukkan URL webhook yang sudah disiapkan.

* **Memastikan Header Permintaan Dikirim ke Webhook:** Hasura mengirimkan header autentikasi (misalnya, Authorization) ke webhook untuk memverifikasi status autentikasi pengguna.

* **Menguji dan Debugging:** Lakukan uji coba untuk memastikan respons webhook diterima dengan benar dan Hasura mendapatkan informasi sesi yang sesuai.

Dengan pendekatan ini, autentikasi dapat dikelola secara terpisah, memberikan fleksibilitas dalam mengelola identitas dan peran pengguna.

## Custom Business Logic Hasura V3

![image](https://github.com/user-attachments/assets/b1ce7b27-a02c-4830-aa61-28567230f97f)

Di Hasura v3, Custom Business Logic Hasura V3 dapat ditulis langsung di dalam Hasura menggunakan bahasa seperti Go, TypeScript, atau Python. Logika ini disimpan dalam metadata Hasura dan terintegrasi langsung, tanpa perlu menghubungkan layanan eksternal. Ini mempermudah pengelolaan dan meningkatkan keamanan, karena semua logika dikelola dalam Hasura.

## Private Deployment

**Hasura-Hosted (VPC)**
https://hasura.io/docs/3.0/deployment/private/hasura-hosted

![image](https://github.com/user-attachments/assets/7469cec1-024f-4f5b-a955-3a97057a913a)

**Hasura-Hosted (VPC)** adalah layanan Hasura yang mengelola deployment, uptime, dan ketersediaan data plane untuk Anda. Layanan ini tersedia di cloud seperti GCP, AWS, dan Azure, dan bisa dideploy di berbagai wilayah untuk mengurangi latensi ke klien Anda.

Data plane beroperasi di infrastruktur komputasi dan jaringan yang terisolasi untuk meningkatkan keamanan dan kepatuhan. Anda bisa menghubungkan jaringan pribadi menggunakan opsi seperti VPC Network Peering atau Private Link untuk keamanan ekstra.

**Self-Hosted (BYOC)**

![image](https://github.com/user-attachments/assets/da14780d-3e89-4cfe-8034-0beb9f64008f)

**Dalam Hasura DDN Self-Hosted:**

https://hasura.io/docs/3.0/deployment/private/self-hosted

* **Data Plane** berjalan di infrastruktur private (misalnya Kubernetes), menangani trafik API dan data tanpa keluar dari jaringan internal. memiliki kendali sepenuhnya terhadap uptime dan updates.

* **Control Plane** mengelola konfigurasi dan metadata sistem, dengan komunikasi terbatas dengan data plane untuk skenario tertentu. Data tidak pernah keluar dari data plane.

![image](https://github.com/user-attachments/assets/78eb02a1-9228-4e4a-b3ab-dec11c65d764)

Menggambarkan interaksi antara `data plane` dan `control plane` dalam konteks Hasura-Managed Data Plane:

* Data Plane mengakses bucket penyimpanan metadata untuk mengambil artefak build yang diperlukan untuk menjalankan aplikasi.
* Data Plane juga mengakses API control plane untuk mendapatkan informasi terkait build yang diterapkan, yang berguna untuk routing data.
* Data Plane mengirimkan data observability (seperti log dan metrik) ke control plane agar data tersebut dapat divisualisasikan di console untuk monitoring dan analisis.
* Control plane mengelola workload data plane melalui interaksi dengan cluster Kubernetes (khusus untuk Hasura-Managed Data Plane), memastikan aplikasi berjalan dengan baik.
  
Pada intinya, control plane bertanggung jawab untuk mengelola data plane, sedangkan data plane berfungsi untuk menangani aplikasi dan observabilitas.

## Keuntungan Menggunakan Hasura Data Delivery Network

* Peningkatan manajemen metadata: Metadata dikelola lebih cepat dengan perubahan instan dan tanpa masalah cold-start.
* Penerapan cepat: Deployment CI/CD bisa dilakukan dalam hitungan detik, tanpa downtime.
* Alur kerja berbasis kode: Perkakas pembuat kode yang canggih dengan spesifikasi tunggal untuk API.
* Kontrol penuh: Pembuatan metadata deklaratif dan kontrol skema API.
* Tanpa basis data metadata: Mengurangi beban manajemen.
* Integrasi data: Menghubungkan ke berbagai sumber data dan logika bisnis dengan konektor asli.
* Supergraf terhubung: Menggabungkan API dan data menjadi satu supergraf yang kuat.
* Kolaborasi tim: Kontrol versi dan fitur kolaborasi untuk bekerja lebih efisien.
* Performa tinggi: Eksekusi kueri yang dioptimalkan dan caching untuk skalabilitas.
* API global: Latensi rendah dan performa tinggi melalui jaringan pengiriman data (DDN).
* Penggunaan bahasa pilihan: Menyusun logika bisnis menggunakan TypeScript dan lainnya

## Feature API V2 Dan V3

**Tabel Dari Segi API**

![Feature API V2   V3](https://github.com/user-attachments/assets/6faa9f1f-1f88-45b0-8e27-84a3fb62bc90)

* EE: Fitur hanya tersedia di Cloud dan Enterprise edition.
* C: Didukung oleh connector tertentu.
* WIP: Fitur masih dalam tahap pengembangan (Work In Progress)

### Berikut penjelasan singkat mengenai fitur yang ada di Hasura v2 dan Hasura DDN (v3):

* **Instant GraphQL API:** Keduanya mendukung pembuatan API GraphQL secara instan.
* **Multiple Data Sources:** Mendukung berbagai sumber data, baik di v2 maupun v3.
* **Query, Mutation, Subscription:** Semua tersedia, tetapi di v3 beberapa fitur seperti subscription dan streaming masih dalam pengembangan.
* **Aggregate Query:** Tersedia di keduanya, namun di v3 lebih dioptimalkan (C berarti fitur lanjutan).
* **Native Mutation:** Hanya tersedia di v3.
* **Action:** Di v3 digantikan oleh Lambda Connectors.
* **Event Trigger dan Cron Trigger:** Event trigger sedang dikerjakan di v3, dan cron trigger tidak ada di v3.
* **Remote Schema:** Lebih mudah dikelola di v3.
* **CI/CD:** Sepenuhnya didukung di kedua versi.
* **Federation & Apollo Federation:** Sepenuhnya didukung di kedua versi.
* **API Limits & Allow Lists:** API limits dalam pengembangan di v3, sementara allow lists tetap ada.
* **Permissions & Authentication Integrations:** Sama di kedua versi.
* **Admin Secret:** Diganti dengan admin-level token di v3.
* **Relay API & RESTified Endpoints:** Tersedia di v3, tetapi RESTified endpoints sedang dalam pengembangan.
* **Schema Registry & Read Replica:** Tersedia di kedua versi, dengan Read Replica di Enterprise v2.
* **Caching:** Dalam pengembangan di v3.

**Tabel dari segi Tooling**

![image](https://github.com/user-attachments/assets/909ae43e-6c62-44db-8637-1d30339e3c4c)

**Fitur Hasura DDN (Dibandingkan dengan v2):**

* **Console:** DDN menggunakan console untuk mengeksplorasi, mengelola, dan mendepploy API, bukan untuk membuatnya. Console kini menawarkan analitik yang lebih baik dan fitur kolaborator.
* **CLI:** CLI sekarang menjadi alat utama untuk membangun API, membuat metadata, dan mengotomatisasi deployment. CLI terintegrasi dengan VS Code untuk mempermudah pengelolaan metadata.
* **Integrasi IDE:** Diperkenalkan untuk memudahkan pengelolaan metadata langsung di editor kode, dimulai dengan VS Code.
* **Migrasi Database:** DDN tidak mendukung migrasi database secara native, tetapi menyarankan alternatif seperti Flyway atau Liquibase.
* **Prometheus:** Didukung secara native dan gratis untuk mesin dan konektor data.
* **OpenTelemetry:** Didukung secara native untuk tracing dan observabilitas, gratis untuk mesin dan konektor data.

