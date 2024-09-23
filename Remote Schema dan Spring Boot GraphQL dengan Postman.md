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

## Analisa Query Graphql
### Schema: todosGraphql
**Query 1: GetAllTodos**
```
query GetAllTodos {
  todographql {
    todos {
      id
      text
      done
      user {
        id
        name
      }
    }
  }
}

```
![image](https://github.com/user-attachments/assets/448020b1-1b8e-48f1-8d58-bba2d5d94a4a)

**Query 2: GetAllUsers**
```
query GetAllUsers {
  todographql {
    users {
      id
      name
    }
  }
}

```
![image](https://github.com/user-attachments/assets/1246efbf-65aa-4a20-a014-6cbc3ffbf5df)


**Query 3: todoByPK**
```
query todoByPK {
  todographql {
    todo(id: "1") {
      done
      id
      text
      user {
        id
        name
      }
    }
    users {
      id
    }
  }
}
```
![image](https://github.com/user-attachments/assets/0ad7c715-d49d-4666-af9a-9c29cf4c94a1)

**Query 4: userByPK**
```
query userByPK {
  todographql {
    user(id: "1") {
      id
      name
    }
  }
}
```
![image](https://github.com/user-attachments/assets/5b45f98e-72f8-4b4a-9518-d1d6a0fc068c)

### Schema: springbootGraphql

**Query 1: countAuthorsAndTutorials**
```
query countAuthorsAndTutorials {
    countAuthors
    countTutorials
  }
```
![image](https://github.com/user-attachments/assets/1410d1d6-22c0-4d46-a81e-b378cd46c859)

**Query 2: getAllAuthors**

```
query getAllAuthors {
    findAllAuthors {
      age
      id
      name
    }
  }

```

![image](https://github.com/user-attachments/assets/5eae98fb-2b17-4645-86d6-cd81e75e33b5)
