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




