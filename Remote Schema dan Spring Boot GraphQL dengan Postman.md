## Remote Schema

**Remote Schema** di GraphQL penggabungan beberapa API GraphQL dari sumber yang berbeda ke dalam satu endpoint. Fungsinya untuk menyederhanakan arsitektur, meningkatkan skalabilitas, dan memudahkan akses ke data terdistribusi melalui satu server GraphQL.

berikut adalah remote schema yang telah saya buat `todos-graphql` yang menggunakan `graphql endpoint` dengan url berikut (http://10.100.14.10:8989/query)
![image](https://github.com/user-attachments/assets/ebb765e2-cee9-4fef-98ef-b8a07f7b4e9a)

## Connect hasura ke Springboot Graphql endpoint dengan remote schema
Berikut Saya Suda Connect menggunakan Remote schema

![image](https://github.com/user-attachments/assets/0a8cbac7-75c3-4701-b0df-a1f37cf7908e)

Pada Bagian API, maka skema yang sebelumnya sudah dibuat di springboot akan muncul dan dapat langsung di jalankan, berikut adalah contoh saya menjalankan query count dan get data tutorial dan authornya

![image](https://github.com/user-attachments/assets/dd77abbf-e544-4994-88f5-14c4d9690bc5)
Pengujian Spring Boot yang terhubung ke Hasura menggunakan Postman dilakukan untuk memastikan interaksi API berjalan dengan baik. Spring Boot berperan sebagai backend yang bisa mengakses API GraphQL Hasura atau langsung ke database.

## Testing Via Postman
Berikut Sudah berjalan di Postman

![image](https://github.com/user-attachments/assets/c47048b9-3bc0-43df-8d4c-3bd7c9d97f2f)

Dengan Postman, bisa menguji endpoint API (seperti GET, POST, dll.) untuk memverifikasi alur data, penanganan error, dan struktur responsnya. Intinya, ini memastikan Spring Boot dan Hasura berfungsi dengan baik dalam integrasi API.

Berikut penjelasan singkat tentang metode HTTP utama:

GET: Mengambil data dari server (baca data).

POST: Mengirim data untuk membuat sumber daya baru di server.

PUT: Memperbarui seluruh sumber daya atau membuatnya jika belum ada.

PATCH: Memperbarui sebagian data dari sumber daya yang ada.

DELETE: Menghapus sumber daya dari server. 
