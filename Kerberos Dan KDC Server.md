**Kerberos** adalah protokol otentikasi jaringan yang dirancang untuk menyediakan keamanan dalam lingkungan jaringan yang tidak aman. Protokol ini bekerja dengan prinsip "trusted third-party authentication," yaitu menggunakan server pusat untuk memverifikasi identitas pengguna dan layanan.

#**Mekanisme Kerberos**
**Komponen Utama Kerberos:**

* **Key Distribution Center (KDC):** Server pusat yang mengelola autentikasi. Terdiri dari dua bagian:
  * **Authentication Server (AS):** Bertugas memverifikasi identitas pengguna.
  * **Ticket Granting Server (TGS):** Memberikan tiket akses ke layanan.
* **Client:** Entitas (biasanya pengguna atau perangkat) yang meminta akses ke layanan.
* **Service/Server:** Layanan atau server yang ingin diakses oleh klien.

**Proses kerja mekanisme Kerberos** 

**1. Autentikasi Awal ke Authentication Server (AS)**
* **Permintaan dari Klien (AS Request):**
Klien mengirimkan permintaan ke Authentication Server (AS) yang ada di KDC untuk membuktikan identitasnya. Permintaan ini meliputi:
  * Nama pengguna (Client ID).
  * Stempel waktu yang terenkripsi dengan kunci rahasia klien (biasanya berasal dari password klien).

* **Respons dari AS (AS Response):**
AS memeriksa identitas klien dengan mencocokkan kredensial yang diterimanya dengan yang ada di database. Jika cocok:
  * AS mengirimkan Ticket Granting Ticket (TGT) ke klien. TGT ini dienkripsi dengan kunci rahasia KDC sehingga hanya KDC yang dapat membaca isinya.
  * AS juga mengirimkan kunci sesi untuk digunakan antara klien dan KDC. Kunci ini dienkripsi dengan kunci rahasia klien

**2. Permintaan Tiket Layanan ke Ticket Granting Server (TGS)**
* **Permintaan dari Klien (TGS Request):**
Jika klien ingin mengakses layanan tertentu, ia mengirimkan permintaan ke Ticket Granting Server (TGS), meliputi:

  * TGT yang diterima dari AS.
  * Informasi tentang layanan yang ingin diakses.
  * Stempel waktu untuk memastikan permintaan masih valid.

* **Respons dari TGS (TGS Response):**
TGS memverifikasi TGT (membaca isinya menggunakan kunci rahasia KDC) dan memeriksa apakah klien diizinkan untuk mengakses layanan tersebut. Jika valid:

  * TGS memberikan tiket layanan yang dienkripsi dengan kunci rahasia layanan tujuan.
  *Tiket layanan ini hanya dapat dibaca oleh layanan yang dimaksud.

**3. Akses ke Layanan**

* **Permintaan dari Klien ke Layanan:**
Klien mengirim tiket layanan ke server atau layanan tujuan, meliputi:

  * Tiket layanan yang diterima dari TGS.
  * Stempel waktu untuk membuktikan bahwa tiket masih valid.

* **Verifikasi oleh Server/Layanan:**
Server membaca tiket layanan menggunakan kunci rahasianya sendiri. Jika tiket valid dan cocok dengan kebijakan akses, server:

  * Membuka sesi komunikasi yang aman dengan klien menggunakan kunci sesi.
  * Memberikan akses ke layanan yang diminta.

**Kesimpulan**
* **AS:** Memberikan TGT setelah autentikasi awal.
* **TGS:** Memberikan tiket layanan untuk akses ke layanan spesifik.
* **Server/Layanan:** Memverifikasi tiket layanan dan memberikan akses.
Semua komunikasi aman karena menggunakan enkripsi berbasis kunci rahasia dan tiket yang hanya dapat dibaca oleh pihak yang sah.
