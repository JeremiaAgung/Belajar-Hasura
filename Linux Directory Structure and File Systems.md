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

# Ringkasan
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

