`systemd` adalah sistem init dan manajer layanan di Linux.

Membuat Unit File
Buat File Unit: Di `/usr/local/bin/hello.py`
```
#!/usr/bin/env python3

import time

while True:
    print("Hello, World!")
    time.sleep(60)

```
Jangan lupa untuk membuat skrip ini bisa dieksekusi:

```
sudo chmod +x /usr/local/bin/hello.py
```
Membuat File Service

Sekarang buat file service di `/etc/systemd/system/hello.service`:
```
sudo nano /etc/systemd/system/hello.service

```

Isi file tersebut dengan:

```
[Unit]
Description=Hello World Service
After=network.target

[Service]
ExecStart=/usr/local/bin/hello.py
Restart=always
User=nobody
Group=nogroup

[Install]
WantedBy=multi-user.target

```

## Mengaktifkan dan Menonaktifkan

Aktifkan: `sudo systemctl enable hello.service`

![image](https://github.com/user-attachments/assets/c7fb9d04-4f46-4f9b-a286-fad0da12719d)

Nonaktifkan: `sudo systemctl disable hello.service`

![image](https://github.com/user-attachments/assets/74dc9ba1-7180-4a4a-82a2-76eaa7e22e29)

Mulai: `sudo systemctl start hello.service`

![image](https://github.com/user-attachments/assets/856b693c-d66a-4737-a4ad-6e43be1a8a95)

Hentikan: `sudo systemctl stop hello.service`

![image](https://github.com/user-attachments/assets/a11f9378-e775-4e2a-864b-a52482422c72)

Periksa Status: `sudo systemctl status hello.service`

![image](https://github.com/user-attachments/assets/20c8b2b5-fc9b-42b3-8f94-4663cce37608)

Nb: Dikarenakan Status dari hello.service di stop

![image](https://github.com/user-attachments/assets/5433ca5d-e9bd-4dc6-b51b-a8b519d68043)

Nb: Dikarenakan Status dari hello.service di start

Reload Konfigurasi: `sudo systemctl daemon-reload`

![image](https://github.com/user-attachments/assets/28f4315d-95f4-4b24-aeb3-f50666a3b384)

## Berikut adalah beberapa perintah dasar Linux yang sering digunakan:

Manajemen File dan Direktori
`ls`: Menampilkan daftar file dan direktori.
`ls`

![image](https://github.com/user-attachments/assets/8f86a418-7d17-4b21-8ca4-e0246fd4315e)

cd: Berpindah direktori.
`cd /hasura-docker`

![image](https://github.com/user-attachments/assets/32bfc920-3e18-4de8-9840-394c870c1fd8)

pwd: Untuk mengetahui lokasi Anda saat ini dalam struktur direktori..
`pwd`

![image](https://github.com/user-attachments/assets/28f1bf23-d410-4d3f-8ef7-29f48d19d89b)

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

![image](https://github.com/user-attachments/assets/ab3321dd-5d2c-4f4a-a314-c43dbee5089c)

`ps`: Menampilkan daftar proses.
`ps aux`

![image](https://github.com/user-attachments/assets/5ca56ad3-d58e-41c7-aacf-07eb7ba6efe2)

df: Menampilkan penggunaan disk.
`df -h`

![image](https://github.com/user-attachments/assets/69c8fbcd-ae9b-4e0c-b1dd-985193d8aa5e)

du: Menampilkan penggunaan ruang disk oleh file atau direktori.
`du -sh /path/to/directory`

free: Menampilkan informasi memori.
`free -h`

![image](https://github.com/user-attachments/assets/5b8250e6-ac8a-490c-9ed5-13c1dbafb153)

## Manajemen Pengguna

`whoami`: Menampilkan nama pengguna saat ini.
`whoami`

![image](https://github.com/user-attachments/assets/f6dd15e0-acf6-4d3c-8eca-65a487203a02)

adduser: Menambahkan pengguna baru.
`sudo adduser username`

![image](https://github.com/user-attachments/assets/5b995bb2-a4be-4071-bdb9-5edae895c19c)

deluser: Menghapus pengguna.
`sudo deluser username`

![image](https://github.com/user-attachments/assets/d56de172-f302-4b77-8269-93227139c8dd)

## Manajemen Paket 
apt-get (Debian/Ubuntu): Mengelola paket.

**Update**: `sudo apt-get update`

![image](https://github.com/user-attachments/assets/34d3c8aa-1bee-4295-bc06-11e7d48bd3d6)

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


