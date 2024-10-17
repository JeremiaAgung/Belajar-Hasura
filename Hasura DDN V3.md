# Hasura DDN 
**Hasura DDN Subgraphs dan Supergraphs**

**Hasura Data Delivery Network (DDN)** memperkenalkan konsep "supergraph" untuk mengatasi masalah fragmentasi data ini. Supergraph adalah kerangka kerja yang menggabungkan berbagai sumber data ke dalam satu API yang aman dan konsisten. Dengan supergraph, dapat menggabungkan:

* **Database relasional**
* **Database non-relasional (NoSQL)**
* **API pihak ketiga**
* **Layanan dan logika bisnis khusus**
Supergraph ini memungkinkan aplikasi untuk bekerja dengan mulus meskipun mereka mengandalkan banyak sumber data dan layanan yang berbeda.

**Subgraphs** dan **supergraphs** di Hasura Data Delivery Network (DDN) memungkinkan pengelolaan GraphQL API yang modular dan skalabel:
* **Subgraphs:** Bagian dari supergraph yang menangani domain tertentu (misalnya, produk, pengguna, pesanan). Setiap subgraph memiliki schema GraphQL sendiri dan dapat dikelola secara terpisah.

* **Supergraphs:** Gabungan dari semua subgraph, menyediakan satu endpoint GraphQL yang mengakses data dari berbagai subgraph. Supergraph mengelola skema gabungan dan merutekan query ke subgraph yang sesuai.

**Keuntungannya:**

* Modularitas dan skalabilitas
* Mempermudah pengelolaan API besar dengan banyak domain
* Memungkinkan tim berbeda bekerja pada subgraph yang berbeda
* 
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


