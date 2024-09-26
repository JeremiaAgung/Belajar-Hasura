# RESTified Endpoints
**RESTified endpoints** adalah cara mudah untuk membuat endpoint REST tanpa perlu menulis kode.bisa mengubah kueri atau mutasi GraphQL menjadi endpoint REST secara otomatis, lengkap dengan parameter dan izin akses. Fitur ini juga memungkinkan untuk mengaktifkan endpoint CRUD (Create, Read, Update, Delete) hanya dengan beberapa klik. Selain itu, bisa mengekspor dokumentasi OpenAPI untuk mempermudah integrasi dengan layanan lain. Ini membuat Developer jadi lebih cepat dan sederhana.

Berikut CreateREST

![image](https://github.com/user-attachments/assets/1c147a4c-be83-4e93-bfa9-90a11b79242e)

Kemudian Output sebagai berikut
![image](https://github.com/user-attachments/assets/1faa5533-1d30-4ca3-ad7f-dfe7ed433cb4)

![image](https://github.com/user-attachments/assets/d1bb8993-1087-489a-ad1b-f2c6a40a346b)

Dengan Cek Di Postman
![image](https://github.com/user-attachments/assets/b6a4fc87-c25d-44b1-b7a7-629ed5e764ce)

Ketika header Key dan Value tidak kita buat akan seperti ini yang terjadi
![image](https://github.com/user-attachments/assets/fe1608a2-7be2-4f57-930e-04e578ac8d66)

# OpenTelemetry Exporter

OpenTelemetry adalah framework yang digunakan untuk mengumpulkan dan mengirimkan data observasi seperti logs, metrics, dan traces dari aplikasi.

Pada bagian gambar ini menjelasan tentang bagaimana status kita buat menjadi enable disable dan variable dengan 

Traces Endpoint  http://10.100.13.205:4317/v1/traces

Metrics Endpoint http://10.100.13.205:4318/v1/metrics

Logs Endpoint http://10.100.13.205:4319/v1/logs

![image](https://github.com/user-attachments/assets/a751dbcb-d06b-4c45-a426-7641aa00114c)
