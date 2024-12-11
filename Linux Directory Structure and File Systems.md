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

### Penjelasan
- **`/`**: Root dari sistem file.
- **`etc`**: Direktori untuk file konfigurasi sistem.
- **`rc.d`**: Subdirektori dari `etc` yang biasanya menyimpan skrip inisialisasi.
- **`init.d`**: Subdirektori dari `rc.d`, digunakan untuk menyimpan skrip start/stop layanan.
- **`functions`**: File yang berisi fungsi yang dapat dipanggil oleh skrip lain dalam direktori `init.d`.


## Direktori Utama dalam Sistem Linux

Pada sistem Linux, direktori utama di bawah direktori root (`/`) dibagi menjadi dua jenis berdasarkan isi datanya:

### **Data Statis**

Data statis adalah data yang tidak berubah dengan sendirinya, kecuali jika diubah secara manual oleh pengguna atau admin. Contoh direktori dengan data statis:

- **`/bin` atau `/usr/bin`**: Berisi file program atau perintah (command) yang digunakan oleh sistem dan pengguna.
- **`/etc`**: Berisi file konfigurasi untuk mengatur sistem.
- **`/lib` atau `/usr/lib`**: Berisi library (fungsi pendukung) yang digunakan oleh program.
- **`/boot`**: Berisi file kernel dan file yang diperlukan saat sistem menyala.
- **`/dev`**: Berisi file perangkat (device files) untuk menghubungkan hardware.

### **Data Dinamis (atau Variabel)**

Data dinamis adalah data yang sering berubah karena aktivitas sistem atau aplikasi. Contoh direktori dengan data dinamis:

- **`/var/log`**: Berisi log file yang mencatat aktivitas sistem atau aplikasi.
- **`/proc`**: Berisi file status yang memberikan informasi real-time tentang proses sistem.
- **`/tmp`**: Berisi file sementara (temporary files) yang dibuat untuk penggunaan jangka pendek oleh program.

Singkatnya, **direktori statis** menyimpan file penting yang sifatnya tetap, sementara **direktori dinamis** menyimpan file yang selalu diperbarui oleh sistem.

---

## Kategori Sistem File di Linux

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


## Sistem File Root (/)

Sistem File Root (/) adalah direktori tingkat atas dalam Filesystem Hierarchy Standard (FHS) yang berisi direktori utama untuk menyimpan informasi tertentu. Berikut beberapa direktori penting:

### Direktori Penting

- **/etc**: Berisi file konfigurasi sistem, termasuk subdirektori seperti:
  - `systemd`: Untuk konfigurasi layanan sistem.
  - `sysconfig`: Konfigurasi sistem lainnya.
  - `lvm`: *Logical Volume Manager*.
  - `skel`: Template *startup* untuk pengguna.

- **/root**: Direktori *home* default untuk pengguna root.

- **/mnt**: Digunakan untuk memasang (*mount*) sistem file sementara.

### Ukuran Sistem File Root

Ukuran sistem file root biasanya ditentukan otomatis oleh program installer berdasarkan ruang disk yang tersedia. Namun, ukuran ini dapat diubah sesuai kebutuhan.

## File Sistem /boot pada Linux

File sistem **/boot** adalah tempat penyimpanan kernel Linux, file pendukung booting, dan konfigurasi boot. Ukuran file sistem ini secara default ditentukan secara otomatis oleh program installer berdasarkan ruang disk yang tersedia. Namun, ukuran ini dapat diatur ulang baik selama proses instalasi maupun setelah instalasi sesuai kebutuhan.

## Penjelasan Direktori-direktori di Sistem UNIX/Linux

Berikut adalah penjelasan singkat mengenai beberapa direktori di sistem UNIX/Linux:

### Direktori Home (/home)
Direktori ini digunakan untuk menyimpan direktori home pengguna dan file pribadi mereka. Setiap pengguna memiliki direktori home sendiri untuk menyimpan file dan dapat membatasi akses pengguna lain ke dalamnya.

### Direktori Opsional (/opt)
Direktori ini digunakan untuk menyimpan perangkat lunak tambahan yang diinstal pada sistem. Setiap perangkat lunak yang diinstal akan memiliki subdirektori tersendiri.

### Direktori Sumber Daya Sistem UNIX (/usr)
Direktori ini berisi sebagian besar file sistem penting. Beberapa subdirektorinya adalah:

- **/usr/bin:** Menyimpan file eksekusi penting untuk pengguna.
- **/usr/sbin:** Menyimpan perintah sistem yang memerlukan hak akses root untuk dijalankan.
- **/usr/lib dan /usr/lib64:** Menyimpan pustaka bersama yang dibutuhkan oleh perintah dan aplikasi lainnya.
- **/usr/include:** Menyimpan file header untuk bahasa pemrograman C.
- **/usr/local:** Digunakan oleh administrator untuk menyimpan perangkat lunak yang diunduh atau dikembangkan sendiri.
- **/usr/share:** Menyimpan dokumentasi, manual, dan file konfigurasi yang dapat dibagikan antar platform Linux.
- **/usr/src:** Menyimpan kode sumber.

Direktori-direktori ini memiliki fungsi yang berbeda untuk mengelola sistem dan perangkat lunak di dalamnya, serta menyediakan ruang untuk file pengguna dan program sistem yang diperlukan.

## Direktori `/var` dalam Sistem Linux

Direktori `/var` menyimpan data yang sering berubah selama sistem berjalan. File-file dalam direktori ini berisi data yang dinamis seperti log, status, spool, lock, dan lainnya. Beberapa subdirektori umum di bawah `/var` adalah:

### `/var/log`
Direktori ini menyimpan sebagian besar file log sistem, seperti:
- Log sistem
- Log boot
- Log pengguna
- Log kegagalan pengguna
- Log instalasi
- Log cron
- Log email
- Dan banyak lagi.

### `/var/opt`
Direktori ini menyimpan file log, status, dan data variabel lainnya untuk perangkat lunak tambahan yang diinstal di direktori `/opt`.

### `/var/spool`
Direktori ini berisi direktori yang menyimpan pekerjaan yang antre, seperti:
- Pekerjaan cetak
- Pekerjaan cron
- Pesan email
- Dan item yang antre lainnya yang akan dikirim ke tujuan mereka.

### `/var/tmp`
Direktori ini menyimpan file sementara yang lebih besar atau file sementara yang perlu ada untuk waktu yang lebih lama daripada yang biasanya diizinkan di direktori sementara lain seperti `/tmp`. File-file ini akan bertahan setelah reboot sistem dan akan dihapus secara otomatis jika tidak diakses atau dimodifikasi dalam periode 30 hari.

## Penjelasan Sistem File Virtual di Linux

### Direktori Temporary (/tmp)
Direktori ini digunakan untuk menyimpan file sementara yang dibuat oleh berbagai program saat runtime atau instalasi. File ini akan bertahan meskipun sistem melakukan reboot dan akan dihapus otomatis jika tidak diakses atau dimodifikasi dalam waktu 10 hari.

### File Sistem Perangkat (/dev), Virtual
Direktori `/dev` menyimpan file perangkat untuk perangkat keras fisik dan perangkat virtual. Kernel Linux berkomunikasi dengan perangkat ini melalui node perangkat yang ada di direktori ini. Node perangkat dikelola oleh layanan `udevd`.

Terdapat dua jenis file perangkat:
- **Perangkat Karakter (Character devices)**: Diakses secara serial, contoh seperti keyboard, printer, dan terminal.
- **Perangkat Blok (Block devices)**: Diakses secara paralel, contoh seperti hard disk, optical drives, dan printer paralel.

### File Sistem Procfs (/proc), Virtual
Direktori `/proc` menyimpan informasi tentang status kernel yang sedang berjalan, termasuk konfigurasi hardware, status CPU, memori, disk, partisi, jaringan, dan proses yang sedang berjalan. File di dalamnya bersifat pseudo (tidak benar-benar ada di disk) dan dikelola secara dinamis oleh sistem.

### File Sistem Runtime (/run), Virtual
Direktori `/run` digunakan untuk menyimpan data dari proses yang sedang berjalan. Salah satu subdirektorinya, `/run/media`, digunakan untuk secara otomatis memasang file sistem eksternal seperti pada USB atau CD/DVD. Konten di dalamnya dihapus saat sistem dimatikan.

### File Sistem Sysfs (/sys), Virtual
Direktori `/sys` menyimpan informasi tentang perangkat keras, driver, dan fitur kernel. Ini digunakan untuk memuat dukungan perangkat yang diperlukan, membuat node perangkat di `/dev`, dan mengonfigurasi perangkat. File sistem ini juga dikelola secara otomatis oleh sistem.

## Memahami Mekanisme Perintah di Linux

Untuk berlatih perintah yang diberikan dalam bab ini, dapat masuk sebagai user1, menjalankan perintah, dan mengamati output-nya. Namun, karena sedang mempelajari administrasi sistem Linux, penting untuk merasa nyaman bekerja sebagai root di awal. Jika ada yang rusak, server1 dan server2 adalah server lab yang dapat dibangun kembali.

### Sintaks Dasar Perintah Linux

Sintaks dasar perintah Linux adalah:

- **Opsi (switch atau flag)** adalah opsional. dapat menentukan nol atau lebih opsi dengan sebuah perintah. 
- **Argumen**, sebaliknya, bisa opsional atau wajib tergantung pada perintah dan penggunaannya. Banyak perintah memiliki opsi dan argumen default yang sudah diprakekkan, jadi tidak perlu menyebutkannya. Perintah lain mengharuskan setidaknya satu opsi atau argumen agar berfungsi.
- **Opsi** mengubah perilaku perintah. **Argumen** adalah target untuk menjalankan aksi perintah.

### Format Opsi
- **Format pendek** opsi dimulai dengan satu tanda hubung (-), seperti `-la` yang berarti dua opsi (`l` dan `a`).
- **Format panjang** opsi dimulai dengan dua tanda hubung (--), seperti `--all` yang merupakan satu opsi.

### Contoh Perintah dan Penjelasan

- `# ls`  
  Tanpa opsi dan argumen eksplisit; argumen default adalah direktori saat ini.
  
- `# ls -l`  
  Satu opsi, tanpa argumen eksplisit; argumen default adalah direktori saat ini.
  
- `# ls -al`  
  Dua opsi, tanpa argumen eksplisit; argumen default adalah direktori saat ini.
  
- `# ls --all`  
  Satu opsi, tanpa argumen eksplisit; argumen default adalah direktori saat ini.
  
- `# ls -l directory_name`  
  Satu opsi, satu argumen eksplisit.

## Perintah `ls` di Linux

Perintah `ls` digunakan untuk menampilkan daftar file dan direktori di Linux. Berikut adalah beberapa opsi yang sering digunakan:

| Opsi  | Deskripsi |
|-------|-----------|
| `-a`  | Menampilkan file dan direktori tersembunyi (dimulai dengan `.`). |
| `-l`  | Menampilkan daftar rinci, termasuk tipe file, izin akses, pemilik, grup, ukuran, dan waktu modifikasi. |
| `-ld` | Menampilkan rincian tentang direktori tanpa menampilkan isinya. |
| `-lh` | Menampilkan rincian dengan ukuran file yang lebih mudah dibaca (misalnya dalam KB, MB). |
| `-lt` | Mengurutkan file berdasarkan tanggal dan waktu, file terbaru di atas. |
| `-ltr` | Mengurutkan file berdasarkan tanggal dan waktu, file terlama di atas (urutan terbalik). |
| `-R`  | Menampilkan isi direktori dan subdirektorinya secara rekursif. |

## Navigasi Direktori di Linux

### Menampilkan Direktori Aktif
Perintah `pwd` (print working directory) digunakan untuk menampilkan lokasi direktori saat ini. Contoh output yang menunjukkan pengguna root berada di direktori `/root`:

Direktori `/root` adalah direktori home untuk pengguna root. Perintah `pwd` selalu mengembalikan path absolut dari file atau direktori.

## Menavigasi Direktori
File disimpan dalam berbagai direktori di Linux, dan setiap file atau direktori memiliki path yang unik. Path (atau pathname) adalah cara untuk mengidentifikasi lokasi file atau direktori dalam struktur direktori.

### Path Absolut
Path absolut (atau path lengkap) menunjuk ke file atau direktori dari root direktori (`/`). Path ini selalu diawali dengan tanda garis miring `/`.

### Path Relatif
Path relatif menunjuk ke file atau direktori berdasarkan lokasi saat ini. Path ini tidak dimulai dengan `/`. Path relatif bisa menggunakan tanda dua titik (`..`) untuk naik satu level ke direktori induk, atau dengan nama subdirektori tanpa garis miring, misalnya `etc/sysconfig`.

### Contoh Penggunaan `cd` dan `pwd`
Menampilkan direktori saat ini dan pindah satu level ke atas:
   ```
   pwd     # Menampilkan direktori saat ini (/root)
   cd ..   # Pindah satu level ke direktori induk (/)
   pwd     # Menampilkan direktori baru (/)
   cd /etc/sysconfig    # Menggunakan path absolut
   cd sysconfig         # Menggunakan path relatif
   cd      # Kembali ke direktori home
   cd ~    # Kembali ke direktori home
   ```

### 1. **Mengidentifikasi File Perangkat Terminal**
Linux menggunakan file perangkat bernomor unik yang disebut pseudo terminal files di direktori `/dev/pts` untuk mewakili sesi terminal pengguna. Perintah `tty` digunakan untuk mengidentifikasi sesi terminal aktif, yang akan menampilkan file perangkat seperti `/dev/pts/0`.

### 2. **Memeriksa Uptime dan Beban Prosesor Sistem**
Perintah `uptime` digunakan untuk memeriksa waktu sistem saat ini, durasi sistem telah berjalan, jumlah pengguna yang sedang login, dan rata-rata beban CPU selama 1, 5, dan 15 menit terakhir. Beban CPU diukur dengan angka load average, di mana angka lebih besar dari 1 menunjukkan beban berlebih pada sistem.

### 3. **Membersihkan Layar Terminal**
Perintah `clear` atau shortcut `Ctrl+l` digunakan untuk membersihkan layar terminal, memudahkan untuk menjalankan perintah baru di layar yang bersih.

### 4. **Menentukan Jalur Perintah**
Untuk mengetahui jalur absolut perintah yang dijalankan, dapat menggunakan perintah `which`, `whereis`, dan `type`. Perintah `which` menunjukkan lokasi file eksekusi, `whereis` memberikan informasi lebih lengkap tentang file biner dan manualnya, dan `type` memberi tahu apakah perintah tersebut adalah built-in shell atau program eksternal beserta jalurnya.

---

### Melihat Informasi Sistem

Perintah `uname` digunakan untuk mengetahui informasi dasar tentang sistem, termasuk nama host.

### Perintah `uname`

- Jika perintah `uname` dijalankan tanpa opsi apapun, hanya nama sistem operasi yang akan ditampilkan.
- Namun, jika menambahkan opsi `-a`, perintah ini akan menampilkan informasi lebih lengkap tentang sistem.

### Contoh Perintah `uname -a`

```
bash $ uname -a
Linux server1.example.com 4.18.0-80.el8.x86_64 #1 SMP Wed Mar 13 12:02:46 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```
## Mengakses Manual Pages di Linux

Manual pages (`man`) adalah dokumentasi yang menyediakan informasi tentang perintah dan aplikasi di Linux. Berikut adalah beberapa navigasi dasar yang dapat digunakan saat membaca manual pages:

### Navigasi Manual Pages:
- **Enter / Down arrow**: Memindahkan ke baris berikutnya.
- **Up arrow**: Memindahkan ke baris sebelumnya.
- **f / Spacebar / Page down**: Memindahkan satu halaman ke depan.
- **b / Page up**: Memindahkan satu halaman ke belakang.
- **d / u**: Memindahkan setengah halaman ke bawah / ke atas.
- **g / G**: Pergi ke awal / akhir halaman man.
- **:f**: Menampilkan nomor baris dan byte yang sedang dilihat.
- **q**: Keluar dari manual page.
- **/pattern**: Mencari ke depan untuk pola yang ditentukan.
- **?pattern**: Mencari ke belakang untuk pola yang ditentukan.
- **n / N**: Menemukan pencarian berikutnya / sebelumnya dari pola.
- **h**: Menampilkan bantuan tentang tombol navigasi.

## Perintah `info` dan `pinfo`

Berikut adalah beberapa perintah yang dapat digunakan dalam `info` dan `pinfo` untuk menjelajah dokumentasi:

- **Down / Up arrows**: Pindah satu baris ke bawah / ke atas.
- **Spacebar / Del**: Pindah satu halaman ke depan / ke belakang.
- **q**: Keluar dari tutorial.
- **[ / ]**: Pindah ke node sebelumnya / selanjutnya dalam dokumen.
- **t**: Pindah ke node paling atas dalam dokumen.
- **s**: Mencari string ke depan.
- **{ / }**: Mencari kemunculan string sebelumnya / selanjutnya.

