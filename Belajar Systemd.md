`systemd` adalah sistem init dan manajer layanan di Linux.

Membuat Unit File
Buat File Unit: Di `/etc/systemd/system/ (misalnya, myservice.service)`
```
[Unit]
Description=Deskripsi Layanan

[Service]
ExecStart=/path/to/executable
Restart=always

[Install]
WantedBy=multi-user.target
```

## Mengaktifkan dan Menonaktifkan

Aktifkan: `sudo systemctl enable myservice.service`

Nonaktifkan: `sudo systemctl disable myservice.service`

Mulai: `sudo systemctl start myservice.service`

Hentikan: `sudo systemctl stop myservice.service`

Periksa Status: `sudo systemctl status myservice.service`

Reload Konfigurasi: `sudo systemctl daemon-reload`

## Berikut adalah beberapa perintah dasar Linux yang sering digunakan:

Manajemen File dan Direktori
`ls`: Menampilkan daftar file dan direktori.
`ls`

cd: Berpindah direktori.
`cd /path/to/directory`

pwd: Menampilkan direktori kerja saat ini.
`pwd`

cp: Menyalin file atau direktori.
`cp source destination`

mv: Memindahkan atau mengganti nama file atau direktori.
`mv source destination`

rm: Menghapus file atau direktori.
`rm file`
`rm -r directory`

## Manajemen Sistem
`top`: Menampilkan proses yang sedang berjalan.
`top`

`ps`: Menampilkan daftar proses.
`ps aux`

df: Menampilkan penggunaan disk.
`df -h`
du: Menampilkan penggunaan ruang disk oleh file atau direktori.
`du -sh /path/to/directory`

free: Menampilkan informasi memori.
`free -h`

## Manajemen Pengguna

`whoami`: Menampilkan nama pengguna saat ini.
`whoami`

adduser: Menambahkan pengguna baru.
`sudo adduser username`

deluser: Menghapus pengguna.
`sudo deluser username`

## Manajemen Paket 
apt-get (Debian/Ubuntu): Mengelola paket.
**Update**: `sudo apt-get update`
**Install**: `sudo apt-get install package`
**Remove**: `sudo apt-get remove package`
**yum** (Red Hat/CentOS): Mengelola paket.
**Update**: `sudo yum update`
**Install**: `sudo yum install package`
**Remove**: `sudo yum remove package`

## Jaringan
`ping`: Mengirim ping ke host untuk memeriksa konektivitas.
`ping hostname`

`ifconfig`: Menampilkan konfigurasi jaringan (sekarang sering digantikan oleh ip).
`ifconfig`

`ip`: Menampilkan atau mengkonfigurasi informasi jaringan.

`ip addr show`

## Izin Akses

`chmod`: Mengubah izin file atau direktori.
`chmod 755 file`

`chown`: Mengubah pemilik dan grup file atau direktori.
`chown user:group file`

## Syntax pada terminal Linux

`ls` - Menampilkan daftar file dan direktori

`ls` - Menampilkan file dan direktori di direktori saat ini
`ls -l` - Menampilkan daftar dengan detail tambahan
`ls -a` - Menampilkan semua file, termasuk file tersembunyi

`cd` - Mengubah direktori

`cd /path/to/directory` - Berpindah ke direktori yang ditentukan
`cd ..` - Kembali ke direktori parent
`cd ~`- Pindah ke direktori home pengguna

`pwd` - Menampilkan direktori kerja saat ini

`cp` - Menyalin file atau direktori
`cp source destination` - Menyalin file atau direktori dari sumber ke tujuan
`cp -r source_dir destination_dir` - Menyalin direktori beserta isinya

`mv` - Memindahkan atau mengganti nama file atau direktori
`mv source destination` - Memindahkan atau mengganti nama file atau direktori

`rm` - Menghapus file atau direktori
rm file - Menghapus file
rm -r directory - Menghapus direktori dan isinya

`mkdir` - Membuat direktori baru
`mkdir directory_name` - Membuat direktori baru dengan nama yang ditentukan

`rmdir` - Menghapus direktori kosong
`rmdir directory_name` - Menghapus direktori kosong

`touch` - Membuat file kosong baru atau memperbarui timestamp file
`touch file_name` - Membuat file baru atau memperbarui file yang sudah ada

`cat` - Menampilkan isi file
`cat file` - Menampilkan isi file ke terminal

`grep` - Mencari teks dalam file
`grep pattern file` - Mencari pola di dalam file

`chmod` - Mengubah hak akses file atau direktori
`chmod permissions file` - Mengatur hak akses file

`chown` - Mengubah pemilik dan grup file atau direktori
`chown owner:group file` - Mengubah pemilik dan grup file

`ps` - Menampilkan informasi tentang proses yang berjalan
ps` - Menampilkan proses untuk pengguna saat ini
`ps aux` - Menampilkan semua proses

`kill` - Menghentikan proses
`kill PID` - Menghentikan proses dengan PID tertentu

`man` - Menampilkan halaman manual untuk perintah
`man command` - Menampilkan halaman manual untuk perintah yang diberikan


