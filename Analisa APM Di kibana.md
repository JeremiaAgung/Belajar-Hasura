#APM

## **APM (Application Performance Monitoring)** 
di Kibana adalah modul yang digunakan untuk memantau kinerja aplikasi secara real-time. Dengan APM, dapat melacak permintaan, latensi, error, dan performa aplikasi secara mendalam, sehingga membantu dalam:

* **Mengidentifikasi Bottleneck**
Dapat melihat bagian mana dari aplikasi yang memperlambat sistem, seperti query lambat, fungsi mahal, atau masalah lain yang memengaruhi performa.

* **Monitoring End-to-End**
APM memungkinkan melacak alur lengkap dari suatu permintaan, mulai dari frontend hingga backend dan database, sehingga Anda memahami perjalanan permintaan secara keseluruhan.

* **Mendeteksi Error**
dapat menangkap error atau exception yang terjadi di aplikasi dan melihat trace-nya untuk memahami akar penyebabnya.

## **Cara Kerja APM di Kibana**

**Agent**
perlu menginstal APM Agent di aplikasi. Agent ini tersedia untuk berbagai bahasa pemrograman seperti Node.js, Java, Python, dan lain-lain. Agent mengumpulkan data terkait permintaan, error, dan performa.

**APM Server**
Agent mengirimkan data ke APM Server, yang merupakan bagian dari Elastic Stack. APM Server memproses data sebelum menyimpannya ke Elasticsearch.

**Kibana APM UI**
Data yang sudah disimpan di Elasticsearch ditampilkan melalui Kibana dalam bentuk grafik, heatmap, dan trace untuk membantu analisis lebih mudah.

## **Fitur Utama APM di Kibana**

**Transaction Monitoring:** Melihat performa berbagai transaksi aplikasi.
**Service Map:** Visualisasi hubungan antar layanan di aplikasi Anda.
**Trace:** Melihat detail langkah-langkah yang diambil suatu permintaan.
**Error Monitoring:** Laporan error beserta konteksnya.
**Metrics:** Memonitor metrik sistem seperti CPU dan memori.
