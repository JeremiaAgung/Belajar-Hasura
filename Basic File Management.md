# Memahami Jenis-Jenis File di Linux

Linux mendukung berbagai jenis file yang dapat diidentifikasi berdasarkan data yang disimpan. Pemahaman ini penting bagi pengguna dan administrator.

## Jenis File Utama
1. **File Teks dan Biner**: Menyimpan data dalam format teks atau biner.
2. **File Perangkat**: Menyimpan informasi perangkat keras.
3. **File Simbolik (Symbolic Link)**: Menunjuk ke data yang sama pada disk.

## Kompresi dan Arsip
- **Manfaat**: Menghemat ruang disk, mempercepat transfer.
- **Proses**: File dapat dengan mudah diekstrak kembali.
- **Alat**: RHEL menyediakan alat bawaan untuk kompresi dan arsip.

## Penyuntingan File Teks
- **Editor**: `vim` populer di komunitas Linux.
- **Keahlian**: Penting untuk pengguna dan administrator.

## Operasi Umum pada File dan Direktori
- Operasi: Membuat, menyalin, memindahkan, mengganti nama, menghapus.
- **Catatan**: Hak istimewa lebih tinggi diperlukan untuk wilayah di luar akses pengguna.

## Link pada File dan Direktori
- **Link**: Menghubungkan ke data tanpa membuat salinan.
- **Salinan**: Digunakan untuk file independen.

# Penjelasan tentang Direktori dan Output `ls -l`

Direktori adalah wadah logis yang menyimpan file dan subdirektori. Perintah `ls -l` digunakan untuk menampilkan daftar isi direktori beserta informasi detailnya. Berikut adalah contoh output dari perintah `ls -l` yang menunjukkan beberapa direktori dalam `/usr/bin`:
```
total 224
drwxr-xr-x 2 root root 40960 Aug 22 2016 bin
drwxr-xr-x 8 root root 12288 Dec 16 2020 games
drwxr-xr-x 2 root root 16384 Jul 4 2016 lib
drwxr-xr-x 2 root root 12288 Aug 26 2016 local
```
Huruf "d" pada awal setiap entri baris menunjukkan bahwa entri tersebut adalah sebuah direktori. Anda dapat mencoba menjalankan perintah `file` dan `stat` pada `/usr` untuk melihat informasi lebih lanjut tentang direktori ini.

# File Perangkat di Sistem Unix-like

Di sistem Unix-like, file perangkat di direktori `/dev` digunakan untuk berkomunikasi dengan perangkat keras. Terdapat dua jenis file perangkat:

## 1. File Perangkat Karakter
- **Ditandai dengan:** `c` (contoh: `crw-------`)
- **Fungsi:** Mengizinkan data dibaca dan ditulis secara karakter per karakter. Cocok untuk perangkat yang mengirimkan data sebagai aliran byte, seperti keyboard dan mouse.
- **Contoh:** `/dev/console` adalah file perangkat karakter untuk konsol sistem.

## 2. File Perangkat Blok
- **Ditandai dengan:** `b` (contoh: `brw-r-----`)
- **Fungsi:** Mengizinkan data dibaca dan ditulis dalam blok (potongan data berukuran tetap). Digunakan untuk perangkat yang menyimpan data dalam blok, seperti hard disk dan SSD.
- **Contoh:** `/dev/sda`, `/dev/sda1`, dll., adalah file perangkat blok yang mewakili perangkat penyimpanan.

## Ringkasan
Dalam contoh yang diberikan:
- Entri pertama (`/dev/console`) adalah perangkat karakter, ditandai dengan `c`.
- Entri berikutnya (`/dev/sda`, `/dev/sda1`, dll.) adalah perangkat blok, ditandai dengan `b`.

Perbedaan ini memungkinkan sistem operasi untuk mengelola berbagai perangkat secara efisien berdasarkan karakteristik penanganan datanya.

# Symbolic Links

**Symbolic Link** (atau **soft link** atau **symlink**) adalah jenis tautan yang bertindak sebagai pintasan menuju file atau direktori lain. 

Jika Anda menjalankan perintah `ls -l` pada file atau direktori yang terhubung secara simbolis, entri daftar akan dimulai dengan huruf "l", dan sebuah panah akan menunjukkan tautan target. 

Contoh penggunaan dapat dilihat pada perintah berikut:

```bash
[root@server1 ~]# ls -l /usr/sbin/vigr
lrwxrwxrwx. 1 root root 4 Dec 18 2018 /usr/sbin/vigr -> vipw
```
# Panduan Penggunaan `gzip` dan `gunzip` di Linux

## Pendahuluan
`gzip` digunakan untuk mengompresi file, sedangkan `gunzip` untuk mendekompresi. File yang dikompresi akan memiliki ekstensi `.gz`.

## Langkah-Langkah

# Kompresi dan Dekompresi File Menggunakan Gzip

## 1. Menyalin File
Sebelum melakukan kompresi, salin file ke lokasi tujuan:

```bash
cp /etc/fstab /root
```

Periksa file yang telah disalin:

```bash
ls /root
```

## 2. Kompresi File
Lakukan kompresi pada file menggunakan gzip:

```bash
gzip /root/fstab
```

Periksa file yang telah terkompresi:

```bash
ls /root
```

## 3. Melihat Informasi Kompresi
Untuk melihat detail informasi file terkompresi, gunakan opsi `-l`:

```bash
gzip -l /root/fstab.gz
```

## 4. Dekompresi File
Dekompresi file yang telah dikompresi menggunakan gunzip:

```bash
gunzip /root/fstab.gz
```

Periksa file setelah dekompresi:

```bash
ls -l /root
```

## Ringkasan Perintah
Berikut adalah ringkasan perintah yang digunakan:

| Perintah                          | Deskripsi                          |
|-----------------------------------|------------------------------------|
| `cp /etc/fstab /root`             | Menyalin file                     |
| `ls /root`                        | Menampilkan daftar file           |
| `gzip /root/fstab`                | Mengompresi file                  |
| `gzip -l /root/fstab.gz`          | Melihat informasi file terkompresi|
| `gunzip /root/fstab.gz`           | Mendekompresi file                |
| `ls -l /root`                     | Memeriksa atribut file            |

# Panduan Penggunaan `bzip2` dan `bunzip2`

`bzip2` digunakan untuk mengompresi file ke format `.bz2`, sedangkan `bunzip2` digunakan untuk mendekompresinya.

## Langkah-Langkah

### 1. Kompresi File
Gunakan `bzip2` untuk mengompresi file:
```bash
bzip2 nama_file
```
Contoh:
```bash
bzip2 fstab
```
Setelah kompresi, file akan menjadi `fstab.bz2`.

### 2. Verifikasi File
Periksa file hasil kompresi:
```bash
ls
```
Hasil:
```text
fstab.bz2
```

### 3. Dekompresi File
Gunakan `bunzip2` untuk mendekompresi file:
```bash
bunzip2 nama_file.bz2
```
Contoh:
```bash
bunzip2 fstab.bz2
```
Setelah dekompresi, file asli akan muncul kembali tanpa ekstensi `.bz2`.

## Catatan
- File asli akan **hilang** setelah dikompresi.
- Gunakan `bunzip2` untuk mengembalikan file ke bentuk semula.

# Menggunakan `tar`

Perintah `tar` (tape archive) digunakan untuk membuat, menambahkan, memperbarui, mencantumkan, dan mengekstrak file atau seluruh struktur direktori ke dan dari satu file, yang disebut sebagai tarball atau tarfile. Perintah ini juga dapat diinstruksikan untuk mengompresi tarball setelah dibuat.

`tar` mendukung banyak opsi.

## Opsi `tar`

| Opsi | Definisi |
|------|----------|
| `-c` | Membuat tarball. |
| `-f` | Menentukan nama tarball. |
| `-p` | Mempertahankan izin file. Default untuk pengguna root. Tentukan opsi ini jika Anda membuat arsip sebagai pengguna biasa. |
| `-r` | Menambahkan file ke akhir tarball tidak terkompresi yang sudah ada. |
| `-t` | Mencantumkan isi dari tarball. |
| `-u` | Menambahkan file ke akhir tarball tidak terkompresi yang sudah ada jika file yang ditambahkan lebih baru. |
| `-v` | Mode verbose. |
| `-x` | Mengekstrak atau mengembalikan dari tarball. |
