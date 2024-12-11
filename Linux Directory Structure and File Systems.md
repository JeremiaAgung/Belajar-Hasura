# Linux Filesystem Hierarchy

Sistem file Linux diatur secara hierarkis untuk memudahkan administrasi dan pengenalan struktur. **Red Hat Enterprise Linux** mengikuti Filesystem Hierarchy Standard (**FHS**), yang menentukan nama, lokasi, dan izin untuk berbagai tipe file dan direktori.

Struktur direktori Linux mirip dengan pohon terbalik, di mana akar (**root**) berada di atas dan diwakili oleh karakter garis miring (`/`). Setiap cabang adalah subdirektori, dan setiap daun adalah file. Garis miring juga digunakan sebagai pemisah direktori dalam sebuah jalur, misalnya:

```
/etc/rc.d/init.d/functions
```

Pada jalur tersebut:

1. **Direktori `etc`**
   - Subdirektori dari root (`/`).

2. **Direktori `rc.d`**
   - Anak dari `etc`.

3. **Direktori `init.d`**
   - Anak dari `rc.d`.

4. **File `functions`**
   - Merupakan "daun" di bawah `init.d`.

## Visualisasi Hierarki Direktori
Berikut adalah representasi visual dari jalur tersebut:

```
/
├── etc
    ├── rc.d
        ├── init.d
            ├── functions
```

## Penjelasan
- **`/`**: Root dari sistem file.
- **`etc`**: Direktori untuk file konfigurasi sistem.
- **`rc.d`**: Subdirektori dari `etc` yang biasanya menyimpan skrip inisialisasi.
- **`init.d`**: Subdirektori dari `rc.d`, digunakan untuk menyimpan skrip start/stop layanan.
- **`functions`**: File yang berisi fungsi yang dapat dipanggil oleh skrip lain dalam direktori `init.d`.


# Direktori Utama dalam Sistem Linux

Pada sistem Linux, direktori utama di bawah direktori root (`/`) dibagi menjadi dua jenis berdasarkan isi datanya:

## **Data Statis**

Data statis adalah data yang tidak berubah dengan sendirinya, kecuali jika diubah secara manual oleh pengguna atau admin. Contoh direktori dengan data statis:

- **`/bin` atau `/usr/bin`**: Berisi file program atau perintah (command) yang digunakan oleh sistem dan pengguna.
- **`/etc`**: Berisi file konfigurasi untuk mengatur sistem.
- **`/lib` atau `/usr/lib`**: Berisi library (fungsi pendukung) yang digunakan oleh program.
- **`/boot`**: Berisi file kernel dan file yang diperlukan saat sistem menyala.
- **`/dev`**: Berisi file perangkat (device files) untuk menghubungkan hardware.

## **Data Dinamis (atau Variabel)**

Data dinamis adalah data yang sering berubah karena aktivitas sistem atau aplikasi. Contoh direktori dengan data dinamis:

- **`/var/log`**: Berisi log file yang mencatat aktivitas sistem atau aplikasi.
- **`/proc`**: Berisi file status yang memberikan informasi real-time tentang proses sistem.
- **`/tmp`**: Berisi file sementara (temporary files) yang dibuat untuk penggunaan jangka pendek oleh program.

Singkatnya, **direktori statis** menyimpan file penting yang sifatnya tetap, sementara **direktori dinamis** menyimpan file yang selalu diperbarui oleh sistem.

---

# Kategori Sistem File di Linux

Terdapat tiga jenis utama sistem file yang didukung di RHEL (Red Hat Enterprise Linux):

## **1. Sistem File Berbasis Disk**
Sistem file ini dibuat di media fisik seperti hard drive atau flash drive USB. Data yang disimpan bersifat permanen, kecuali dihapus secara manual. Contohnya adalah partisi `root` dan `boot` yang dibuat selama instalasi RHEL.

## **2. Sistem File Berbasis Jaringan**
Sistem file ini berbasis disk, tetapi dibagikan melalui jaringan untuk akses jarak jauh oleh perangkat lain. Contohnya adalah Network File System (NFS).

## **3. Sistem File Berbasis Memori**
Sistem file ini bersifat virtual, dibuat secara otomatis saat sistem menyala, dan akan dihapus saat sistem dimatikan. Data di dalamnya tidak disimpan secara permanen (hilang setelah reboot). Contohnya adalah direktori `/proc` dan `/tmp`.

---

### Ringkasan
- **Direktori Statis**: Berisi file yang tidak berubah seperti file konfigurasi dan program.
- **Direktori Dinamis**: Berisi file yang selalu diperbarui oleh sistem, seperti log file dan file status.
- **Sistem File Linux**: Terdiri dari tiga jenis utama yaitu berbasis disk, jaringan, dan memori.


# Sistem File Root (/)

Sistem File Root (/) adalah direktori tingkat atas dalam Filesystem Hierarchy Standard (FHS) yang berisi direktori utama untuk menyimpan informasi tertentu. Berikut beberapa direktori penting:

## Direktori Penting

- **/etc**: Berisi file konfigurasi sistem, termasuk subdirektori seperti:
  - `systemd`: Untuk konfigurasi layanan sistem.
  - `sysconfig`: Konfigurasi sistem lainnya.
  - `lvm`: *Logical Volume Manager*.
  - `skel`: Template *startup* untuk pengguna.

- **/root**: Direktori *home* default untuk pengguna root.

- **/mnt**: Digunakan untuk memasang (*mount*) sistem file sementara.

## Ukuran Sistem File Root

Ukuran sistem file root biasanya ditentukan otomatis oleh program installer berdasarkan ruang disk yang tersedia. Namun, ukuran ini dapat diubah sesuai kebutuhan.

# File Sistem /boot pada Linux

File sistem **/boot** adalah tempat penyimpanan kernel Linux, file pendukung booting, dan konfigurasi boot. Ukuran file sistem ini secara default ditentukan secara otomatis oleh program installer berdasarkan ruang disk yang tersedia. Namun, ukuran ini dapat diatur ulang baik selama proses instalasi maupun setelah instalasi sesuai kebutuhan.

# Penjelasan Direktori-direktori di Sistem UNIX/Linux

Berikut adalah penjelasan singkat mengenai beberapa direktori di sistem UNIX/Linux:

## Direktori Home (/home)
Direktori ini digunakan untuk menyimpan direktori home pengguna dan file pribadi mereka. Setiap pengguna memiliki direktori home sendiri untuk menyimpan file dan dapat membatasi akses pengguna lain ke dalamnya.

## Direktori Opsional (/opt)
Direktori ini digunakan untuk menyimpan perangkat lunak tambahan yang diinstal pada sistem. Setiap perangkat lunak yang diinstal akan memiliki subdirektori tersendiri.

## Direktori Sumber Daya Sistem UNIX (/usr)
Direktori ini berisi sebagian besar file sistem penting. Beberapa subdirektorinya adalah:

- **/usr/bin:** Menyimpan file eksekusi penting untuk pengguna.
- **/usr/sbin:** Menyimpan perintah sistem yang memerlukan hak akses root untuk dijalankan.
- **/usr/lib dan /usr/lib64:** Menyimpan pustaka bersama yang dibutuhkan oleh perintah dan aplikasi lainnya.
- **/usr/include:** Menyimpan file header untuk bahasa pemrograman C.
- **/usr/local:** Digunakan oleh administrator untuk menyimpan perangkat lunak yang diunduh atau dikembangkan sendiri.
- **/usr/share:** Menyimpan dokumentasi, manual, dan file konfigurasi yang dapat dibagikan antar platform Linux.
- **/usr/src:** Menyimpan kode sumber.

Direktori-direktori ini memiliki fungsi yang berbeda untuk mengelola sistem dan perangkat lunak di dalamnya, serta menyediakan ruang untuk file pengguna dan program sistem yang diperlukan.

# Direktori `/var` dalam Sistem Linux

Direktori `/var` menyimpan data yang sering berubah selama sistem berjalan. File-file dalam direktori ini berisi data yang dinamis seperti log, status, spool, lock, dan lainnya. Beberapa subdirektori umum di bawah `/var` adalah:

## `/var/log`
Direktori ini menyimpan sebagian besar file log sistem, seperti:
- Log sistem
- Log boot
- Log pengguna
- Log kegagalan pengguna
- Log instalasi
- Log cron
- Log email
- Dan banyak lagi.

## `/var/opt`
Direktori ini menyimpan file log, status, dan data variabel lainnya untuk perangkat lunak tambahan yang diinstal di direktori `/opt`.

## `/var/spool`
Direktori ini berisi direktori yang menyimpan pekerjaan yang antre, seperti:
- Pekerjaan cetak
- Pekerjaan cron
- Pesan email
- Dan item yang antre lainnya yang akan dikirim ke tujuan mereka.

## `/var/tmp`
Direktori ini menyimpan file sementara yang lebih besar atau file sementara yang perlu ada untuk waktu yang lebih lama daripada yang biasanya diizinkan di direktori sementara lain seperti `/tmp`. File-file ini akan bertahan setelah reboot sistem dan akan dihapus secara otomatis jika tidak diakses atau dimodifikasi dalam periode 30 hari.


