## Remote Schema

**Remote Schema** di GraphQL penggabungan beberapa API GraphQL dari sumber yang berbeda ke dalam satu endpoint. Fungsinya untuk menyederhanakan arsitektur, meningkatkan skalabilitas, dan memudahkan akses ke data terdistribusi melalui satu server GraphQL.

berikut adalah remote schema yang telah saya buat `todos-graphql` yang menggunakan `graphql endpoint` dengan url berikut (http://10.100.14.10:8989/query)
![image](https://github.com/user-attachments/assets/ebb765e2-cee9-4fef-98ef-b8a07f7b4e9a)

## Connect to hasura using remote schema
Berikut Saya Suda Connect menggunakan Remote schema

![image](https://github.com/user-attachments/assets/3feebe72-aa42-4b14-8dea-3bb345707732)

Pada Bagian API, maka skema yang sebelumnya sudah dibuat di springboot akan muncul dan dapat langsung di jalankan, berikut adalah contoh saya menjalankan query count dan get data tutorial dan authornya

![image](https://github.com/user-attachments/assets/dd77abbf-e544-4994-88f5-14c4d9690bc5)

## Testing Via Postman
Berikut Sudah berjalan di Postman

![image](https://github.com/user-attachments/assets/c47048b9-3bc0-43df-8d4c-3bd7c9d97f2f)
