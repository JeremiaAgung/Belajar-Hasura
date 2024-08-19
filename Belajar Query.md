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
