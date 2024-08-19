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

**Mengaktifkan dan Menonaktifkan**

Aktifkan: `sudo systemctl enable myservice.service`
Nonaktifkan: `sudo systemctl disable myservice.service`
Mulai: `sudo systemctl start myservice.service`
Hentikan: `sudo systemctl stop myservice.service`
Periksa Status: `sudo systemctl status myservice.service`
Reload Konfigurasi: `sudo systemctl daemon-reload`





