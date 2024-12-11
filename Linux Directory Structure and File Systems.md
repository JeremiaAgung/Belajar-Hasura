Sistem file Linux diatur secara hierarkis untuk memudahkan administrasi dan pengenalan struktur. Red Hat Enterprise Linux mengikuti Filesystem Hierarchy Standard (FHS), yang menentukan nama, lokasi, dan izin untuk berbagai tipe file dan direktori. Struktur direktori Linux mirip dengan pohon terbalik, di mana akar (root) berada di atas dan diwakili oleh karakter garis miring (/). Setiap cabang adalah subdirektori, dan setiap daun adalah file. Garis miring juga digunakan sebagai pemisah direktori dalam sebuah jalur, misalnya `/etc/rc.d/init.d/functions`.

Pada jalur tersebut:

Direktori etc adalah subdirektori dari root (/).

Direktori `rc.d` adalah anak dari `etc`.

Direktori `init.d` adalah anak dari `rc.d`.

File functions adalah "daun" di bawah `init.d`.

## Top-Level Directories

Di sistem Linux, ada beberapa direktori utama yang berada di bawah direktori root `(/)`. Direktori ini dibagi menjadi dua jenis berdasarkan isi datanya:

**Data Statis**

Data statis adalah data yang tidak berubah dengan sendirinya, kecuali diubah secara manual oleh pengguna atau admin. Contohnya:

Perintah (command) seperti file program di `/bin` atau `/usr/bin`.

File konfigurasi di `/etc` yang digunakan untuk mengatur sistem.

Library di `/lib` atau `/usr/lib` yang berisi fungsi pendukung untuk program.

File kernel di `/boot` yang digunakan saat sistem menyala.

File perangkat (device files) di `/dev` untuk menghubungkan hardware.


**Data Dinamis (atau Variabel)**

Data dinamis adalah data yang sering berubah karena aktivitas sistem atau aplikasi. Contohnya:

Log file di `/var/log`, yang mencatat aktivitas sistem atau aplikasi.

File status di `/proc`, yang memberikan informasi real-time tentang proses sistem.

File sementara (temporary files) di `/tmp`, yang dibuat untuk penggunaan jangka pendek oleh program.

Singkatnya, **direktori statis** menyimpan file penting yang sifatnya tetap, sementara **direktori dinamis** menyimpan file yang selalu diperbarui oleh sistem.

## File System Categories

Terdapat tiga jenis utama sistem file yang didukung di RHEL: berbasis `disk`, berbasis `jaringan`, dan berbasis `memori`.

**Sistem file berbasis disk:** Dibuat di media fisik seperti hard drive atau flash drive USB. Data disimpan secara permanen.

**Sistem file berbasis jaringan:** Sistem file berbasis disk yang dibagikan melalui jaringan untuk akses jarak jauh.

**Sistem file berbasis memori:** Virtual, dibuat otomatis saat sistem dinyalakan, dan dihapus saat sistem dimatikan. Data di sini tidak disimpan secara permanen (hilang setelah reboot).

Selama instalasi RHEL dengan partisi default, dua sistem file berbasis disk akan dibuat, yaitu `root` dan `boot`. Selain itu, beberapa sistem file berbasis memori juga penting untuk operasi sistem RHEL.

## The Root File System (/), Disk-Based
