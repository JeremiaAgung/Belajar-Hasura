# Hasura DDN 
**Hasura DDN dan Supergraph**

**Hasura Data Delivery Network (DDN)** memperkenalkan konsep "supergraph" untuk mengatasi masalah fragmentasi data ini. Supergraph adalah kerangka kerja yang menggabungkan berbagai sumber data ke dalam satu API yang aman dan konsisten. Dengan supergraph, dapat menggabungkan:

* **Database relasional**
* **Database non-relasional (NoSQL)**
* **API pihak ketiga**
* **Layanan dan logika bisnis khusus**
Supergraph ini memungkinkan aplikasi untuk bekerja dengan mulus meskipun mereka mengandalkan banyak sumber data dan layanan yang berbeda.

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



