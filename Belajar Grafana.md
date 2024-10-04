# GRAFANA
Grafana terhubung ke Prometheus untuk visualisasi data metrics. Anda dapat membuat dashboard dan grafik menggunakan query PromQL untuk memantau aplikasi atau infrastruktur secara real-time, termasuk alerting berbasis metrics.

## Dashboard Hasura HTTP GraphQL
### Overview
Pada Bagian Overview panel terdapat 7 dashborad  
![image](https://github.com/user-attachments/assets/67adbd98-57ba-4cd8-91ee-dfff17423822)

tampilan dashboard Grafana yang menunjukkan metrics terkait Hasura HTTP GraphQL, yang diambil dari data Prometheus.

* **Total Queries**: Menampilkan 48 query yang telah dijalankan.
* **Query Latency (P95)**: Waktu latensi untuk 95% dari query adalah 28,8 ms.
* **Total Mutations**: Ada 1 operasi mutasi yang telah dilakukan.
* **Mutation Latency (P95)**: Latensi mutasi (P95) adalah 9,50 ms.
* **Top Queries dan Top Mutations**: Tidak ada data spesifik yang ditampilkan di bagian ini selain servis `hasuraferdy` yang terdaftar.
* **Top Error Rate**: Tidak ada data yang error
Grafana memvisualisasikan data ini untuk memantau performa dan responsivitas Hasura.

### GraphQL Metrics
**Query Request Rate**

Untuk menampilkan request rate pada Grafana, biasanya data dikumpulkan dari Prometheus, yang memonitor aplikasi atau service. Langkah-langkah berikut bisa ikuti untuk membuat query request rate di Grafana:
![image](https://github.com/user-attachments/assets/16e7e979-aafc-4680-a318-4f0d33198965)

**Mutation Request rate**

Mutation request rate adalah jumlah permintaan perubahan data (mutations) yang diterima server per waktu. Ini digunakan untuk memantau kinerja, beban server, dan perencanaan skala aplikasi.
![image](https://github.com/user-attachments/assets/83aa5b00-611f-4ca8-8e74-a20a74af77fe)

**Query Error Rate**
Query error rate adalah persentase permintaan (queries) yang gagal atau menghasilkan error dibandingkan dengan total query yang dilakukan dalam suatu periode waktu. Metrik ini penting untuk memantau Healt dan kinerja sistem.
![image](https://github.com/user-attachments/assets/bcc905ed-5533-4c23-ba25-58afb17a583b)

**Mutation Error rate**

Mutation error rate adalah persentase permintaan perubahan data (mutations) yang gagal atau menghasilkan error dibandingkan dengan total mutation yang dilakukan dalam periode waktu tertentu. Metrik ini membantu dalam memantau keandalan dan kinerja operasi yang mengubah data di aplikasi.
![image](https://github.com/user-attachments/assets/2d6730fc-5e1b-4573-858b-c16aa7ee7b44)

**Query Latency (P95) & Mutation Lacency (P95)**
* **Query Latency (P95)** adalah waktu yang dibutuhkan untuk memproses 95% dari semua permintaan query, membantu mengidentifikasi permintaan yang berkinerja buruk.

* **Mutation Latency** adalah waktu yang diperlukan untuk memproses permintaan perubahan data (mutations) hingga selesai. 

Keduanya penting untuk memantau performa dan responsivitas sistem.
![image](https://github.com/user-attachments/assets/fee9ec55-f1ab-4916-8107-14683e72010a)

### General Metrics
![image](https://github.com/user-attachments/assets/724e886b-f852-41f1-8dc4-26acef82a700)
* **HTTP Connection**

Metrik ini mencakup semua permintaan HTTP yang diterima oleh server Hasura, yang mengindikasikan aktivitas API GraphQL. Ini membantu Anda memahami bagaimana aplikasi berinteraksi dengan Hasura.

* **Cache Request Rate**
Cache Request Rate dalam metrik General Metrics di Hasura merujuk pada frekuensi permintaan yang dilayani dari cache dibandingkan dengan permintaan total.Cache Request Rate yang rendah dapat menunjukkan kebutuhan untuk mengoptimalkan strategi caching.

* **HTTP Data Transfer**
metrik yang mengukur jumlah dan efisiensi data yang ditransfer antara client dan server Hasura melalui permintaan HTTP. Dengan memahami data transfer, dapat mengidentifikasi masalah dan mengoptimalkan aplikasi untuk kinerja yang lebih baik.

* **Action Data Transfer**
pada metrik yang melacak jumlah dan ukuran data yang ditransfer terkait dengan Actions yang didefinisikan dalam Hasura. Actions adalah fungsi kustom yang dapat Anda buat di Hasura untuk menangani logika bisnis yang tidak dapat dilakukan hanya dengan kueri GraphQL standar.


## Dashboard Hasura Health
![image](https://github.com/user-attachments/assets/d2094a88-f065-4981-95df-eda2536bfab5)

Hasura Health di Grafana adalah cara untuk memantau kesehatan layanan Hasura GraphQL Engine

**Metadata Status (CONSISTENT):** Ini menunjukkan bahwa metadata di Hasura dalam kondisi konsisten, yang berarti tidak ada masalah sinkronisasi atau ketidaksesuaian dalam metadata yang disimpan dan diakses oleh Hasura.

**Health Check using infinity (OK):** Laporan ini menunjukkan bahwa pengecekan kesehatan layanan menggunakan sumber data atau metode infinity menunjukkan status OK, yang berarti layanan ini berjalan dengan normal.

**Health Check using block (No data):** Pada bagian ini, ada informasi "No data" yang menandakan tidak ada data yang tersedia atau diambil untuk pengecekan kesehatan dengan metode atau sumber data block. Ini bisa berarti bahwa pengukuran belum dimulai atau tidak ada data yang diterima dari sumber tersebut.

**Source Health Check:**

* **default (hasuraferdy) OK:** Sumber health check yang dinamai default menunjukkan status OK, berarti layanan tersebut beroperasi dengan normal pada instance ini.

* **testsejuta (hasuraferdy) OK:** Sumber health check lain yang disebut testsejuta juga menunjukkan status OK, yang berarti tidak ada masalah dalam layanan yang diuji.

**Metadata Version (292):** Ini menunjukkan versi metadata yang sedang digunakan oleh Hasura saat ini, yaitu versi 292. Versi ini penting untuk memastikan kompatibilitas dan integritas fitur-fitur Hasura.

**Health Check Latency:** Tidak ada data yang ditampilkan pada bagian ini, yang mungkin berarti latensi belum diukur atau belum ada data latensi yang diterima.

**Postgres Connections:** Bagian ini juga menunjukkan "No data", yang menunjukkan bahwa koneksi ke database PostgreSQL belum dilaporkan atau tidak ada data koneksi yang tersedia pada saat itu.
