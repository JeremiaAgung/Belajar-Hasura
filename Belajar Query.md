### SQL

1. `SELECT`
Digunakan untuk memilih data dari database. Data yang diambil akan ditampilkan dalam bentuk tabel.

Sintaks:
```
SELECT column1, column2, ...
FROM table_name;
```
Contoh:
`SELECT UserName, UserID
FROM Users;`

2. WHERE
Digunakan untuk memfilter hasil query berdasarkan kondisi tertentu.

Sintaks:
`
SELECT column1, column2, ...
FROM table_name
WHERE condition;
`
Contoh:

```
SELECT UserName
FROM Users
WHERE UserID = 1;
```

3. `ORDER BY`
Digunakan untuk mengurutkan hasil query berdasarkan satu atau lebih kolom.

Sintaks:
`
SELECT column1, column2, ...
FROM table_name
ORDER BY column1 [ASC|DESC];`

Contoh:
```
SELECT UserName
FROM Users
ORDER BY UserName ASC;
```

4. `INSERT INTO`
Digunakan untuk menambahkan baris baru ke dalam tabel.

Sintaks:

`INSERT INTO table_name (column1, column2, ...)
VALUES (value1, value2, ...);`
Contoh:
```
INSERT INTO Users (UserID, UserName)
VALUES (1, 'John Doe');
```

5. `UPDATE`
Digunakan untuk mengubah data yang ada di dalam tabel.

Sintaks:
`UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;`
Contoh:
```
UPDATE Users
SET UserName = 'Jane Doe'
WHERE UserID = 1;
```

6. `DELETE`
Digunakan untuk menghapus baris dari tabel.

Sintaks:
`DELETE FROM table_name
WHERE condition;`
Contoh:
```
DELETE FROM Users
WHERE UserID = 1;
```

7. `CREATE TABLE`
Digunakan untuk membuat tabel baru di dalam database.

Sintaks:
`CREATE TABLE table_name (
    column1 datatype constraint,
    column2 datatype constraint,
    ...
);`
Contoh:
```
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    UserName VARCHAR(100)
);
```

8. `ALTER TABLE`
Digunakan untuk memodifikasi tabel yang sudah ada, seperti menambahkan kolom atau mengubah struktur tabel.

Sintaks:
`ALTER TABLE table_name
ADD column_name datatype;`
Contoh:
```
ALTER TABLE Users
ADD Email VARCHAR(255);
```

9. `DROP TABLE`
Digunakan untuk menghapus tabel dari database beserta semua datanya.

Sintaks:
`DROP TABLE table_name;`
Contoh:
```
DROP TABLE Users;
```

## 1. Primary Key
Primary key adalah kolom atau kombinasi kolom dalam sebuah tabel yang secara unik mengidentifikasi setiap baris dalam tabel tersebut. Setiap nilai dalam kolom primary key harus unik dan tidak boleh ada nilai yang NULL.
Contoh:

Misalkan kita memiliki tabel `Mahasiswa` seperti berikut:
![image](https://github.com/user-attachments/assets/a30106f4-5665-400b-913e-cf5a11f4e477)

Di sini, kolom `NIM` (Nomor Induk Mahasiswa) berfungsi sebagai primary key karena setiap NIM adalah unik untuk setiap mahasiswa.

```
CREATE TABLE Mahasiswa (
    NIM INT PRIMARY KEY,
    Nama VARCHAR(50),
    Jurusan VARCHAR(50)
);

```

## 2. Foreign Key
Foreign key adalah kolom atau kombinasi kolom dalam sebuah tabel yang mengacu pada primary key di tabel lain. Foreign key digunakan untuk menjaga konsistensi data dan menjalin hubungan antar tabel.

Contoh:

Misalkan kita juga memiliki tabel `Pendaftaran` yang mencatat mata kuliah yang diambil oleh mahasiswa:

![image](https://github.com/user-attachments/assets/3e196e3c-3ef0-48a1-b285-45ea9b0b7e66)

Di sini, kolom `NIM` di tabel `Pendaftaran` adalah foreign key yang mengacu pada kolom `NIM` di tabel Mahasiswa.
```
CREATE TABLE Pendaftaran (
    ID_Pendaftaran INT PRIMARY KEY,
    NIM INT,
    Mata_Kuliah VARCHAR(50),
    FOREIGN KEY (NIM) REFERENCES Mahasiswa(NIM)
);
```

**Penjelasan:**

**Primary Key:** Menjamin bahwa setiap baris dalam tabel adalah unik dan dapat diidentifikasi secara khusus.

**Foreign Key:** Menjaga integritas referensial antara tabel-tabel yang berbeda, memastikan bahwa setiap nilai foreign key di tabel anak (contoh: Pendaftaran) memiliki nilai yang sesuai di tabel induk (contoh: Mahasiswa).
