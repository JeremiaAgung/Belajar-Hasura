# Drop Database di Production

(https://www.youtube.com/watch?v=crljo33HV4A&ab_channel=ProgrammerZamanNow)

(https://resend.com/blog/incident-report-for-february-21-2024)

**kesimpulan nya:**
### Apa itu Drop Database?
"Drop database" adalah perintah yang digunakan untuk menghapus seluruh database beserta semua tabel, data, dan objek terkait di dalamnya. Ini adalah tindakan yang tidak bisa dibatalkan, dan data yang dihapus tidak dapat dipulihkan tanpa cadangan.

dari sini belajar mengenai Drop Database Di Production mengalami gangguan database selama sekitar 12 jam karena kesalahan dalam migrasi database yang menghapus data dari server produksi. Akibatnya, pengguna tidak dapat mengakses API, mengirim email, atau melihat dashbord.

Proses pemulihan pertama dari cadangan gagal, sehingga pemulihan kedua dilakukan dengan cadangan lain dan memerlukan waktu tambahan 5 jam. Selama proses ini, ada kehilangan data selama 5 menit sebelum database offline.



