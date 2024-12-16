# Manajemen Pengguna dan Aktivitas di RHEL  

## Pemantauan Aktivitas  
- Aktivitas login pengguna dan riwayat reboot sistem dicatat dalam file log.  
- Data dapat digunakan untuk debugging, pengujian, atau audit.  

## Pembuatan Akun Pengguna  
- Setiap pengguna harus memiliki nama pengguna unik dan kata sandi.  
- Informasi akun disimpan di file khusus (tidak dianjurkan untuk diedit manual).  

## Modifikasi Akun  
- Atribut akun dapat dimodifikasi.  
- Akun dapat dihapus jika tidak lagi diperlukan.  

## Akun Layanan  
- Ditambahkan saat layanan diinstal atau secara manual.  
- Tidak memerlukan akses login, hanya untuk mendukung aplikasi.  

# Menampilkan Pengguna yang Sedang Login

Di Linux, Anda dapat menggunakan perintah `who` atau `w` untuk melihat daftar pengguna yang sedang login.

## Perintah `who`
Menampilkan daftar pengguna dari file `/run/utmp`. Contoh:  
```
$ who
user1    tty1         2024-12-16 09:00
user2    pts/0        2024-12-16 09:05 (192.168.1.10)
```
# Perintah `last` di Linux

## Pengertian
Perintah `last` digunakan untuk melihat riwayat login berhasil, logout, dan reboot sistem. Data diambil dari file **wtmp** yang terletak di direktori `/var/log`. File ini mencatat aktivitas seperti:
- Waktu login
- Durasi sesi
- Terminal (tty) yang digunakan

## Contoh Penggunaan

### 1. Melihat seluruh riwayat login, logout, dan reboot
Jalankan perintah berikut di terminal:
```last
username   tty1         Mon Dec 16 10:00   still logged in
username   pts/0        Mon Dec 16 09:45 - 10:00  (00:15)
reboot     system boot  Mon Dec 16 09:30 - 10:15  (00:45)
```
# Viewing History of Failed User Login Attempts

Perintah `lastb` digunakan untuk melihat riwayat upaya login pengguna yang gagal dengan membaca file **btmp** yang ada di direktori `/var/log`. File ini mencatat semua upaya login yang gagal, termasuk nama login, waktu, dan tty (tempat percobaan dilakukan). Untuk menampilkan semua upaya login yang gagal, cukup jalankan perintah `lastb` tanpa argumen. Perintah ini membutuhkan hak akses **root**.

## Contoh Penggunaan

**Menjalankan perintah:**
```sudo lastb
root     tty1    Mon Dec 11 10:20 - 10:21 (00:01)
admin    pts/1   Tue Dec 12 12:45 - 12:46 (00:01)
user123  ssh:notty Tue Dec 12 14:10 - 14:12 (00:02)

```

# Reporting Recent User Login Attempts

Perintah `lastlog` digunakan untuk melaporkan informasi login terbaru dari setiap akun pengguna di sistem. Informasi ini disimpan dalam file `lastlog` yang terletak di direktori `/var/log`. File ini mencatat rincian login pengguna terakhir, termasuk nama pengguna, waktu login, dan port atau terminal yang digunakan. Data yang disimpan ini berguna untuk memantau aktivitas login pengguna.

## Cara Menggunakan

Untuk menggunakan perintah `lastlog`, jalankan perintah berikut di terminal:

```lastlog
Username    Port     From             Latest
root        tty1     :0               Mon Dec 16 14:32:25 +07 2024
user1       pts/0    192.168.1.5      Mon Dec 16 15:14:47 +07 2024
user2       tty2     :0               Mon Dec 16 12:45:00 +07 2024
```
# File Otentikasi Pengguna di RHEL

RHEL (Red Hat Enterprise Linux) mendukung tiga jenis akun pengguna utama: **root**, **normal**, dan **service**.

### Jenis Akun Pengguna
1. **Root**: Pengguna superuser dengan akses penuh ke semua layanan dan fungsi administratif di sistem.
2. **Pengguna Normal**: Pengguna dengan hak akses terbatas yang dapat menjalankan aplikasi yang diizinkan.
3. **Akun Layanan**: Akun yang digunakan untuk menjalankan layanan seperti apache, ftp, mail, dan chrony.

### File Otentikasi Pengguna
Informasi akun pengguna lokal disimpan dalam empat file yang terletak di direktori `/etc`. File-file ini digunakan untuk memverifikasi kredensial pengguna saat login. Berikut adalah file-file yang terlibat:

#### 1. `/etc/passwd`
File ini menyimpan informasi dasar pengguna seperti nama pengguna, UID (User ID), GID (Group ID), direktori home, dan shell yang digunakan. Contoh:
`user1:x:1001:1001:User One:/home/user1:/bin/bash root:x:0:0:root:/root:/bin/bash apache:x:48:48:Apache:/var/www:/sbin/nologin`

#### 2. `/etc/shadow`
File ini menyimpan informasi terkait kata sandi pengguna yang terenkripsi. Formatnya adalah sebagai berikut:
`user1:$6$abc123$xyz456...:18413:0:99999:7::: root:$6$def456$uvw789...:18524:0:99999:7::: apache:*:18524:0:99999:7:::`

#### 3. `/etc/group`
File ini berisi informasi tentang grup pengguna, GID, dan anggota grup. Contoh:
`root:x:0: wheel:x:10:user1,root apache:x:48:`

#### 4. `/etc/gshadow`
File ini berisi informasi grup dan kata sandi grup dalam format terenkripsi. Contoh:
`root:!::: wheel:!::user1,root apache:*:::`

# Penjelasan Tentang File `passwd` di Linux

File `passwd` adalah file teks sederhana yang menyimpan data penting terkait akun pengguna di sistem Linux. Setiap baris dalam file ini mewakili informasi untuk satu akun pengguna, dengan tujuh kolom yang dipisahkan oleh tanda titik dua (`:`). Kolom-kolom tersebut biasanya mencakup informasi berikut:

1. **Nama Pengguna (username)**: Nama yang digunakan untuk login ke sistem.
2. **Password (password)**: Enkripsi dari password pengguna. Pada beberapa sistem modern, ini bisa berisi tanda `x` atau `*` yang menunjukkan bahwa password disimpan di file terpisah.
3. **UID (User ID)**: ID unik yang diberikan kepada setiap pengguna di sistem.
4. **GID (Group ID)**: ID grup utama pengguna.
5. **Info Pengguna (User Info)**: Informasi tambahan tentang pengguna, seperti nama lengkap atau deskripsi lainnya.
6. **Direktori Home (Home Directory)**: Lokasi direktori home pengguna di sistem.
7. **Shell**: Program shell yang digunakan oleh pengguna setelah login, seperti `/bin/bash`.

Contoh baris dalam file `passwd`:

![image](https://github.com/user-attachments/assets/f6f65a96-7409-4483-a2b3-2ab9c0ced28d)

# Shadow Password in RHEL

RHEL (Red Hat Enterprise Linux) memiliki mekanisme kontrol kata sandi yang lebih aman yang disebut *shadow password*. Dengan kontrol ini, kata sandi pengguna di-hash dan disimpan dalam file yang lebih aman, yaitu `/etc/shadow`. Berikut adalah penjelasan lebih lanjut mengenai file ini dan pengaturannya.

## Keamanan File Shadow

Berbeda dengan file `/etc/passwd` yang dapat dibaca oleh semua pengguna, file `/etc/shadow` memiliki pengaturan izin akses yang lebih ketat. File ini tidak dapat diakses oleh pengguna biasa untuk menjaga kerahasiaan data kata sandi. 

## Pengaturan Usia Kata Sandi (Password Aging)

File `/etc/login.defs` digunakan untuk mengonfigurasi pengaturan terkait kata sandi, seperti batasan waktu kedaluwarsa dan periode peringatan. Pengaturan ini diterapkan pada akun pengguna dan dikenal dengan istilah *password aging*. 

## Format File `/etc/shadow`

File `/etc/shadow` berisi informasi autentikasi pengguna dan pengaturan usia kata sandi. Setiap baris dalam file ini berhubungan dengan satu entri di file `/etc/passwd`. Setiap baris di `/etc/shadow` terdiri dari sembilan field yang dipisahkan oleh tanda titik dua (`:`), yang mencakup informasi seperti:

1. **Nama Pengguna**: Nama pengguna yang terdaftar.
2. **Kata Sandi yang Dihash**: Kata sandi yang di-hash dan disimpan di file ini.
3. **Tanggal Terakhir Kata Sandi Diubah**: Tanggal terakhir kata sandi diubah.
4. **Batas Waktu Kedaluwarsa Kata Sandi**: Batas kedaluwarsa kata sandi.
5. **Periode Peringatan**: Periode sebelum kata sandi kedaluwarsa yang memberikan peringatan kepada pengguna.
6. **Periode Grace**: Periode setelah kata sandi kedaluwarsa di mana pengguna masih dapat login.
7. **Batasan Akses**: Jika akun sudah tidak aktif dalam periode tertentu, akun bisa dinonaktifkan.

![image](https://github.com/user-attachments/assets/39c494b8-6ee6-4801-8089-d4e5ecb875dc)

## Kesimpulan

Dengan menggunakan sistem shadow password, RHEL memberikan tingkat keamanan yang lebih tinggi dalam penyimpanan dan pengelolaan kata sandi. Pengaturan terkait usia dan kedaluwarsa kata sandi yang lebih fleksibel memungkinkan administrator untuk mengelola kebijakan kata sandi pengguna secara lebih aman.

# File Grup di Sistem

File grup adalah file teks biasa yang menyimpan informasi penting terkait grup di sistem. Setiap baris dalam file ini menyimpan informasi untuk satu entri grup. 

## User Private Group (UPG)

Setiap pengguna di sistem harus menjadi anggota setidaknya satu grup, yang disebut dengan **User Private Group (UPG)**. Secara default, nama grup cocok dengan nama pengguna yang bersangkutan.

## Grup Tambahan

Grup tambahan dapat dibuat untuk mengelompokkan pengguna dengan kebutuhan akses file yang serupa. 

## Format Baris

Setiap entri grup terdiri dari empat kolom yang dipisahkan oleh tanda titik dua (`:`). 

![image](https://github.com/user-attachments/assets/1598c3a9-7af6-4542-9bb6-d07a1b56f8b5)

# Penjelasan Tentang File /etc/gshadow

File **/etc/gshadow** adalah file yang digunakan untuk menyimpan kata sandi grup yang di-hash dan memberikan perlindungan tambahan pada tingkat grup. Dalam sistem ini, kata sandi grup disimpan dengan cara yang lebih aman, berbeda dengan file grup (/etc/group) yang bersifat dapat dibaca oleh siapa saja dan hanya dapat ditulis oleh pemiliknya. File **/etc/gshadow** memiliki akses yang sangat terbatas (tanpa izin akses sama sekali) untuk melindungi kontennya.

## Format File gshadow

File **/etc/gshadow** terdiri dari empat kolom yang dipisahkan dengan tanda titik dua (`:`) pada setiap baris. Masing-masing kolom ini berhubungan dengan entri yang ada dalam file **/etc/group**.

### Kolom-kolom dalam file gshadow:
1. **Nama Grup** - Nama grup yang bersangkutan.
2. **Kata Sandi yang Di-hash** - Kata sandi grup yang sudah di-hash untuk perlindungan.
3. **Anggota yang Diizinkan** - Daftar anggota yang diizinkan untuk mengakses grup, jika ada.
4. **Anggota yang Dilarang** - Daftar anggota yang dilarang mengakses grup, jika ada.

## Keamanan File gshadow
File **/etc/gshadow** memiliki akses yang sangat terbatas dan hanya dapat diakses oleh pengguna dengan izin khusus untuk melindungi kontennya yang sensitif. Ini berbeda dengan file **/etc/group**, yang dapat dibaca oleh siapa saja tetapi hanya dapat ditulis oleh pemiliknya.

![image](https://github.com/user-attachments/assets/43a8015d-0004-4054-a3bc-c18911284d51)

# Penjelasan tentang Konfigurasi useradd dan login.defs

Perintah `useradd` di Linux menggunakan file konfigurasi `/etc/default/useradd` dan `/etc/login.defs` untuk mengambil nilai default jika tidak ada opsi yang ditentukan pada baris perintah. 

File `/etc/login.defs` juga digunakan oleh perintah lain seperti `usermod`, `userdel`, `chage`, dan `passwd` untuk mengambil konfigurasi terkait, seperti panjang kata sandi dan siklus hidup kata sandi. 

Anda dapat melihat isi file konfigurasi ini dengan menggunakan perintah seperti `cat` atau `less`, atau menampilkan pengaturannya langsung menggunakan perintah `useradd`.

### Contoh perintah:
- Melihat isi file konfigurasi `useradd`:
```
  cat /etc/default/useradd
```

Menampilkan pengaturan `useradd`:
```
useradd -D
```

# Dokumentasi Perintah `useradd`, `usermod`, dan `userdel` di Linux

Perintah-perintah berikut digunakan untuk mengelola akun pengguna di sistem Linux: `useradd`, `usermod`, dan `userdel`. Berikut adalah penjelasan dan contoh penggunaannya.

## 1. Perintah `useradd`

Perintah `useradd` digunakan untuk menambah akun pengguna baru di sistem Linux. Perintah ini akan membuat direktori home untuk pengguna dan menyalin file startup default dari direktori skeleton `/etc/skel`.

### Opsi yang tersedia:
- `-b <direktori>`: Menentukan direktori dasar untuk direktori home pengguna.
- `-c <komentar>`: Menambahkan komentar atau deskripsi untuk pengguna.
- `-d <direktori_home>`: Menentukan path direktori home pengguna.
- `-e <tanggal>`: Menentukan tanggal kedaluwarsa akun pengguna.
- `-f <jumlah_hari>`: Menentukan jumlah hari tidak aktif setelah kata sandi kedaluwarsa sebelum akun dinonaktifkan.
- `-g <GID_grup>`: Menentukan GID grup utama untuk pengguna.
- `-G <grup_tambahan>`: Menentukan grup tambahan yang menjadi anggota pengguna.
- `-k <direktori_skeleton>`: Menentukan direktori skeleton untuk file default pengguna.
- `-m`: Membuat direktori home jika belum ada.
- `-o`: Membuat akun pengguna dengan UID yang sama dengan pengguna lain.
- `-r`: Membuat akun sistem dengan UID di bawah 1000.
- `-s <shell>`: Menentukan shell default untuk pengguna.
- `-u <UID>`: Menentukan UID unik untuk pengguna.

### Contoh penggunaan:
```bash
useradd -m -s /bin/bash -G admin,developer -c "John Doe" johndoe
```

