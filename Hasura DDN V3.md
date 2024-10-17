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








