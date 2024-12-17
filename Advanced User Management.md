# Pengelolaan Akun Pengguna dan Grup di Linux

## Masa Berlaku Password
- Masa berlaku password dapat diatur untuk meningkatkan kontrol login dan password pengguna.
- Pengaturan ini bisa diterapkan untuk pengguna tertentu atau semua pengguna.
- Informasi masa berlaku password disimpan dalam file autentikasi.
- Akun pengguna dapat dikunci sementara atau permanen, dengan opsi untuk membuka kunci jika diperlukan.
- **Catatan:** Hanya pengguna dengan hak akses root yang dapat melakukan pengaturan ini.

## Keanggotaan Grup
- Setiap pengguna dimasukkan ke dalam satu grup saat ditambahkan ke sistem.
- Pengguna dapat ditambahkan ke grup tambahan setelahnya.
- Anggota grup yang sama memiliki hak akses yang sama pada file dan direktori.
- Pengguna lain atau grup lain dapat diberikan akses tambahan sesuai kebutuhan.
- Informasi keanggotaan grup disimpan dalam file autentikasi.

## Beralih Akun Pengguna
- Pengguna dapat beralih ke akun lain, termasuk root, jika mengetahui password akun tujuan.
- Akses ke perintah tertentu dapat diberikan kepada pengguna biasa melalui pengaturan dalam file konfigurasi.

## Kepemilikan File
- Setiap file di sistem memiliki pemilik dan grup pemilik.
- File yang dibuat oleh pengguna otomatis menjadi milik pengguna tersebut.
- Kepemilikan file dapat diubah oleh superuser dan diberikan kepada pengguna lain.

## Hak Akses Root
Pengelolaan ini memerlukan hak akses **root** untuk melakukan:
- Pengaturan masa berlaku password.
- Penguncian dan pembukaan kunci akun.
- Perubahan kepemilikan file.

### Catatan Penting
Pengelolaan akun pengguna dan grup ini penting untuk menjaga keamanan dan pengelolaan akses pada sistem Linux. Pastikan pengaturan dilakukan dengan hati-hati dan sesuai kebutuhan.

# Perintah `chage`

Perintah `chage` digunakan untuk mengatur atau mengubah parameter kedaluwarsa (aging) kata sandi pada sebuah akun pengguna. Perintah ini akan mengubah berbagai bidang di file `shadow` tergantung pada opsi yang digunakan. 

Terdapat banyak pilihan (switch) yang tersedia dalam format pendek maupun panjang.

## Fungsi Utama
Dengan menggunakan `chage`, Anda dapat:
- Mengatur kapan pengguna harus mengganti kata sandi.
- Menentukan batas waktu masa aktif kata sandi.
- Memaksa kata sandi tertentu untuk segera kedaluwarsa.

## Contoh Sintaks
```bash
chage -l username
```

# Perintah `groupadd`, `groupmod`, dan `groupdel` di Linux

Perintah **`groupadd`**, **`groupmod`**, dan **`groupdel`** adalah perintah yang digunakan untuk mengelola grup pengguna di sistem Linux. 
Berikut adalah penjelasan rinci mengenai masing-masing perintah:

## 1. Perintah `groupadd`
Perintah ini digunakan untuk **menambahkan grup baru** ke dalam sistem. 
Saat perintah ini dijalankan, entri baru akan ditambahkan ke file **`/etc/group`** dan **`/etc/gshadow`**.

### Opsi `groupadd`
| **Opsi**            | **Deskripsi**                                                                                                     |
|----------------------|-------------------------------------------------------------------------------------------------------------------|
| **`-g`** atau `--gid` | Menentukan GID (Group ID) yang akan diberikan pada grup baru.                                                    |
| **`-o`** atau `--non-unique` | Membuat grup dengan GID yang sama dengan grup lain (non-unik). Hal ini hanya disarankan untuk situasi tertentu.    |
| **`-r`**            | Membuat grup sistem dengan GID di bawah 1000. Biasanya digunakan untuk proses atau layanan sistem.                |
| **`groupname`**     | Menentukan nama grup yang akan dibuat.                                                                           |

### Contoh Penggunaan
1. **Menambahkan grup baru dengan nama `developers`:**
   ```bash
   sudo groupadd developers
   ```

2. **Menambahkan grup dengan GID tertentu:**
   ```bash
   sudo groupadd -g 1500 managers
   ```

3. **Membuat grup sistem:**
   ```bash
   sudo groupadd -r systemgroup
   ```

---

## 2. Perintah `groupmod`
Perintah ini digunakan untuk **mengubah pengaturan grup yang sudah ada**. Misalnya, mengganti nama grup atau GID.

### Opsi `groupmod`
| **Opsi**            | **Deskripsi**                                                                                     |
|----------------------|-------------------------------------------------------------------------------------------------|
| **`-g`** atau `--gid` | Mengubah GID grup.                                                                             |
| **`-n`** atau `--new-name` | Mengubah nama grup.                                                                         |

### Contoh Penggunaan
1. **Mengubah nama grup dari `developers` menjadi `devteam`:**
   ```bash
   sudo groupmod -n devteam developers
   ```

2. **Mengubah GID grup:**
   ```bash
   sudo groupmod -g 2000 devteam
   ```

---

## 3. Perintah `groupdel`
Perintah ini digunakan untuk **menghapus grup** dari sistem.

### Contoh Penggunaan
1. **Menghapus grup bernama `managers`:**
   ```bash
   sudo groupdel managers
   ```

**Catatan Penting:**
- Sebelum menghapus grup, pastikan tidak ada file atau direktori yang masih memiliki grup tersebut sebagai pemilik.
- Jika grup yang dihapus masih terkait dengan pengguna, sebaiknya modifikasi akun pengguna tersebut sebelum penghapusan.

---

## Kesimpulan
Ketiga perintah ini sangat penting untuk mengelola grup dalam sistem Linux. Dengan menggunakan perintah ini, administrator dapat:
- Menambah grup baru dengan `groupadd`.
- Mengubah pengaturan grup dengan `groupmod`.
- Menghapus grup yang tidak diperlukan dengan `groupdel`.

Pengelolaan grup membantu dalam mengatur hak akses terhadap file dan direktori, sehingga meningkatkan keamanan dan efisiensi sistem.

# Berpindah (atau Mengganti) Pengguna di Sistem  

Meskipun Anda dapat langsung masuk ke sistem sebagai **root**, hal ini **tidak disarankan**. Sebaiknya, masuklah menggunakan akun pengguna biasa terlebih dahulu, lalu beralih ke akun **root** jika diperlukan. Cara ini lebih aman dan menjaga keamanan serta perlindungan sistem. Selain menjadi **root**, Anda juga dapat beralih ke akun pengguna lain. Namun, untuk beralih ke akun target, Anda harus mengetahui kata sandi pengguna tersebut.  

Perintah `su` memungkinkan Anda berpindah ke akun pengguna lain.  

## Beralih ke Akun Root  
Misalnya, Anda sedang masuk sebagai **user1** dan ingin beralih ke akun **root**. Untuk melakukannya tanpa menjalankan *startup scripts* (yang akan dijelaskan lebih lanjut), jalankan perintah berikut:  

```bash
su
```

Masukkan kata sandi **root** saat diminta. Setelah selesai, tekan kombinasi tombol **Ctrl + d** untuk kembali ke akun **user1**.  

Untuk menjalankan perintah `su` sekaligus mengeksekusi *startup scripts* pada akun target, tambahkan tanda hubung (`-`) pada perintah, seperti ini:  

```bash
su -
```

Dengan cara ini, lingkungan kerja akan menyerupai kondisi saat Anda melakukan login langsung ke akun target.  

## Beralih ke Akun Pengguna Lain  
Jika Anda ingin beralih ke akun pengguna lain, misalnya **user100**, gunakan nama pengguna target dalam perintah `su`. Contohnya:  

```bash
su user100
```

Kemudian, masukkan kata sandi untuk akun **user100** saat diminta.  

## Melihat Identitas Pengguna  
Setelah Anda beralih menggunakan perintah `su`, RHEL menyediakan dua alat untuk memeriksa identitas pengguna:  
1. **whoami**: Menunjukkan identitas pengguna saat ini (*effective username*).  
2. **logname**: Menunjukkan identitas pengguna asli yang pertama kali login ke sistem (*original username*).  

### Contoh:  
Misalkan Anda beralih dari **user1** ke **user100** menggunakan `su`. Setelah itu:  
- Jalankan perintah berikut untuk melihat nama pengguna saat ini:  
  ```bash
  whoami
  ```
  Output:  
  ```plaintext
  user100
  ```

- Jalankan perintah ini untuk melihat nama pengguna asli yang pertama kali login:  
  ```bash
  logname
  ```
  Output:  
  ```plaintext
  user1
  ```

Dengan cara ini, Anda dapat memahami perbedaan antara pengguna saat ini dan pengguna asli yang masuk ke sistem.
# Pemilik dan Grup Pemilik di Linux

Dalam sistem Linux, setiap file dan direktori memiliki **pemilik** dan **grup pemilik**. Secara default, pemilik file adalah pengguna yang membuatnya, dan grup pemilik adalah grup pengguna tersebut. Kepemilikan ini dapat diubah menggunakan perintah-perintah berikut.

## Menampilkan Informasi Pemilik dan Grup Pemilik

Untuk melihat pemilik dan grup pemilik file atau direktori, gunakan perintah **long listing** (`ls -l`):

```bash
ls -l file1
```

# Ringkasan Bab

Pada awal bab ini, kita membahas berbagai atribut kedaluwarsa untuk kontrol login pengguna dan kata sandi yang tersedia. Kita juga melihat file yang menyimpan atribut default yang diterapkan pada akun pengguna saat pertama kali dibuat. Atribut default ini dapat diubah jika diperlukan.

Selanjutnya, kita memodifikasi atribut kedaluwarsa untuk akun pengguna tertentu dengan alat yang telah kita pelajari. Kita juga menggunakan alat dengan sepasang flag untuk menonaktifkan dan mengembalikan akses pengguna ke sistem.

Kita mempelajari perintah manajemen grup dan menggunakannya dalam latihan untuk membuat, mengubah, dan menghapus akun grup, serta menambahkan pengguna ke grup tambahan. Perintah manajemen grup ini cukup sederhana dan mudah digunakan, tetapi memerlukan eksekusi oleh pengguna dengan hak istimewa.

Di bagian akhir bab, kita melihat beberapa alat untuk beralih ke akun pengguna lain, termasuk pengguna root, dan menjalankan perintah yang memerlukan hak istimewa sebagai pengguna biasa. Penggunaan alat ini disarankan.

Terakhir, kita membahas kepemilikan dan grup pemilik pada file dan direktori, serta bagaimana cara penugasannya. Kita melakukan latihan untuk memahami siapa yang dapat memodifikasinya dan bagaimana cara melakukannya.
