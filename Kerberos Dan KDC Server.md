**Kerberos** adalah protokol otentikasi jaringan yang dirancang untuk menyediakan keamanan dalam lingkungan jaringan yang tidak aman. Protokol ini bekerja dengan prinsip "trusted third-party authentication," yaitu menggunakan server pusat untuk memverifikasi identitas pengguna dan layanan.

**Komponen Utama Kerberos**
* **KDC (Key Distribution Center):*
Server utama dalam sistem Kerberos yang bertugas mengelola otentikasi dan distribusi kunci. KDC terdiri dari dua komponen:

Authentication Server (AS): Mengautentikasi pengguna dan memberikan Ticket Granting Ticket (TGT).
Ticket Granting Server (TGS): Mengeluarkan tiket akses ke layanan setelah TGT divalidasi.
Principal: Entitas (pengguna atau layanan) yang berkomunikasi di jaringan Kerberos. Setiap principal memiliki nama unik dan kredensial.

Ticket: Mekanisme otorisasi yang digunakan untuk membuktikan identitas tanpa mengirimkan kata sandi.

Client: Pengguna atau aplikasi yang meminta akses ke layanan.

Service: Layanan di jaringan yang ingin diakses oleh client.

Mekanisme Kerberos: Proses 3 Tahap
Tahap 1: Otentikasi Awal (AS Exchange)

Client mengirimkan permintaan ke Authentication Server (AS) di KDC dengan nama pengguna (tanpa kata sandi langsung).
AS memverifikasi identitas client menggunakan database kunci.
Jika valid, AS memberikan TGT (Ticket Granting Ticket) yang dienkripsi dengan kunci utama client.
TGT ini termasuk:
Informasi identitas client.
Masa berlaku tiket.
Kunci sesi (session key).
Tahap 2: Meminta Akses Layanan (TGS Exchange)

Client mengirim TGT ke Ticket Granting Server (TGS) untuk meminta akses ke layanan tertentu.
TGS memverifikasi TGT dan mengeluarkan tiket layanan baru (service ticket) yang dapat digunakan client untuk mengakses layanan.
Tahap 3: Mengakses Layanan (Client/Server Exchange)

Client mengirimkan service ticket ke layanan tujuan.
Layanan memvalidasi tiket menggunakan kunci bersama dengan KDC.
Jika valid, client diberikan akses ke layanan.
Keunggulan Kerberos
Keamanan Tinggi: Tidak ada kata sandi yang dikirim melalui jaringan; semua komunikasi dienkripsi.
Single Sign-On (SSO): Pengguna cukup masuk satu kali untuk mengakses berbagai layanan.
Masa Berlaku Tiket: Tiket memiliki waktu kedaluwarsa, mengurangi risiko penyalahgunaan.
Kerberos KDC Server
KDC adalah pusat dari sistem Kerberos. Perannya meliputi:

Menyimpan informasi pengguna dan layanan di database.
Mendistribusikan kunci sesi dan tiket.
Menjamin keabsahan identitas semua entitas dalam jaringan.
Catatan: Karena KDC adalah komponen kritis, keamanannya sangat penting. Biasanya, KDC diimplementasikan pada server dengan tingkat keamanan tinggi dan sering kali direplikasi untuk redundansi.

Ringkasan Diagram Kerberos
Client ke AS:
Client → AS: Permintaan autentikasi → AS → Client: TGT + session key

Client ke TGS:
Client → TGS: TGT + permintaan akses layanan → TGS → Client: Service Ticket

Client ke Layanan:
Client → Layanan: Service Ticket → Layanan: Akses diberikan

Dengan mekanisme ini, Kerberos memberikan keamanan berbasis tiket yang cepat, aman, dan fleksibel untuk jaringan modern.






