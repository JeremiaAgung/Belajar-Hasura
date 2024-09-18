# Buat Tabel-Tabel dan Relasinya

Di sini kita akan menggunakan tiga tabel: `todos`, `categories`, dan `users`.

![image](https://github.com/user-attachments/assets/2568efe7-0bf4-48e9-bc7a-055a062b6755)

**Tabel `users`**
Tabel ini menyimpan data pengguna.
```
CREATE TABLE users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```
**Tabel `categories`**
Tabel ini menyimpan kategori untuk setiap todo.
```
CREATE TABLE categories (
    category_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

```
**Tabel `todos`**
Tabel ini menyimpan todo list dengan relasi ke `users` dan `categories`.
```
CREATE TABLE todos (
    todo_id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    description TEXT,
    due_date DATE,
    user_id INT,
    category_id INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(user_id) ON DELETE CASCADE,
    FOREIGN KEY (category_id) REFERENCES categories(category_id) ON DELETE SET NULL
);

```

**Create (Insert Data)**
Mutasi GraphQL untuk menambahkan data ke `todos`:
```
mutation {
  insert_todos(objects: {
    title: "Learn GraphQL",
    description: "Understand mutations and queries",
    due_date: "2024-09-20",
    user_id: 1,
    category_id: 2
  }) {
    returning {
      todo_id
      title
    }
  }
}
```

**Read (Fetch Data)**
Query GraphQL untuk mengambil data dari `todos`:
```
query{
  todos {
    todo_id
    title
    description
    due_date
  }
  users {
    username
  }
  categories {
    name
  }
}

```

![image](https://github.com/user-attachments/assets/b6bf5933-11c0-4da8-bc0d-4a978935a224)

**Update (Update Data)**
Mutasi GraphQL untuk mengupdate data di `todos`:
```
mutation {
  update_todos(
    where: {todo_id: {_eq: 1}},
    _set: {title: "Learn GraphQL and Hasura", description: "Updated description"}
  ) 
}

```
![image](https://github.com/user-attachments/assets/7138d44f-eb54-47c0-914b-0eaf8351e0a0)
**Affected row** untuk mengetahui berapa baris yang terpengaruhi oleh mutase bisa tidak menggunakan affected row tetapi harus diganti setidaknya satu field pada output

**Delete (Hapus Data)**
Mutasi GraphQL untuk menghapus data dari `todos`:
```
mutation {
  delete_todos(where: {todo_id: {_eq: 2}}) 
}
```
![image](https://github.com/user-attachments/assets/5a465333-5bd7-4a38-83c9-67cfbcacdc50)


**Penjelasan Singkat**

* **update_todos:** Nama mutasi yang digunakan untuk memperbarui data dalam tabel todos.
  
* **where:** Menentukan kondisi baris mana yang akan diperbarui. Dalam contoh ini, hanya baris dengan id sama dengan 1 yang akan diperbarui.
  
* **_set:** Menentukan kolom mana yang akan diubah dan nilai barunya. Di sini, kolom title diubah menjadi "Judul yang Diperbarui".
  
* **affected_rows:** Mengembalikan jumlah baris yang terpengaruh oleh mutasi ini.
  
* **returning:** Menentukan kolom apa saja yang ingin Anda ambil dari baris yang diperbarui. Dalam contoh ini, id, title, dan due_date akan dikembalikan.

