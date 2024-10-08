# Hasura DDN
**Hasura Data Delivery Network (DDN)** adalah solusi yang bertujuan untuk meningkatkan efisiensi dalam membangun aplikasi generasi berikutnya dengan menyederhanakan akses data yang aman dan efisien. DDN menggunakan arsitektur supergraf data untuk meningkatkan produktivitas pengembang yang bekerja dengan API dan microservices.

* **Bagi API authors**, DDN menyediakan alat untuk pemodelan domain yang fleksibel, integrasi sumber data yang mulus, pengaturan izin keamanan yang mudah, serta dukungan untuk berbagai bahasa pemrograman. 

* **Bagi API Maintainers**, fokusnya pada optimasi kinerja, peluncuran pembaruan yang lancar, independensi CI/CD, dan skalabilitas global. 

* **Bagi API Consumers**, DDN menjamin keandalan, konsistensi, dan kemudahan dalam menemukan serta mengakses data.

Hasura DDN memperkenalkan metode baru yang lebih cepat dan skalabel untuk pembuatan serta pengelolaan API, yang mengubah cara domain data ditangani dalam pengembangan aplikasi modern.


## Arsitektur dan Cara Kerja Hasura Data Delivery Network (DDN)

Hasura DDN dibangun di atas konsep supergraf data, yang memungkinkan pengembangan dan pengelolaan API dengan cepat dan efisien. Supergraf ini menghubungkan berbagai sumber data yang berbeda, dan memungkinkan integrasi data secara mulus ke dalam satu lapisan API.

Berikut adalah gambaran umum cara kerjanya:

**1.Deklaratif dan Otomatis**
DDN menggunakan pendekatan deklaratif untuk membangun API. Ini berarti pengembang cukup mendeklarasikan skema data, sumber data, dan aturan izin yang diperlukan, dan DDN secara otomatis akan menghasilkan API yang dapat diakses. Hal ini mengurangi banyak langkah manual dalam pembuatan API tradisional.

**2.Integrasi Multi-Sumber Data**
DDN memungkinkan komposabilitas data lintas domain yang berbeda, menghubungkan beberapa sumber data seperti database SQL, NoSQL, API REST, layanan eksternal, dan lainnya. Pengembang dapat mengakses dan mengelola data dari berbagai sumber melalui satu API terpadu.

**3.Keamanan dan Kontrol Izin yang Mudah**
Dengan DDN, pengaturan izin dan keamanan API lebih mudah karena mendukung pengontrolan akses granular. Pengembang dapat menentukan siapa yang bisa mengakses data tertentu atau melakukan tindakan tertentu dengan aturan yang jelas, memastikan bahwa API tetap aman.

**4.Performa dan Skalabilitas Tinggi**
DDN dirancang untuk mengoptimalkan kinerja dengan minimal overhead operasional. API yang dibangun dengan DDN dapat menangani berbagai skala aplikasi, dari aplikasi kecil hingga yang berskala global, dengan topologi yang terdistribusi. DDN memanfaatkan edge computing untuk memastikan API tersedia dengan latensi rendah di seluruh dunia.

**5.Federasi CI/CD dan Stabilitas Operasional**
DDN mendukung federasi pipeline CI/CD, yang berarti setiap tim dalam organisasi dapat bekerja secara independen untuk merilis fitur baru tanpa mempengaruhi tim lain. Ini juga memungkinkan pembaruan dilakukan tanpa downtime atau gangguan terhadap aplikasi yang sedang berjalan.

**6.Penemuan dan Pemodelan Domain Data**
DDN menyediakan alat untuk penemuan domain data dengan cepat, memungkinkan pengembang memahami relasi antar domain data dan mempercepat proses onboarding bagi anggota tim baru. Ini juga memfasilitasi pemodelan domain data yang lebih kaya dan komprehensif.

**Cara Kerja Utama:**

* **Koneksi ke Berbagai Sumber Data:** DDN menghubungkan berbagai jenis sumber data (SQL, NoSQL, REST API) dan menyediakan skema API terpadu yang memudahkan pengembang untuk mengakses dan memanipulasi data tanpa perlu membuat API terpisah untuk setiap sumber data.
Declarative API: Pengembang mendefinisikan skema dan aturan API secara deklaratif, dan DDN otomatis menghasilkan API sesuai dengan kebutuhan tersebut.

* **Federated Architecture:** Arsitektur DDN mendukung distribusi API dan memungkinkan CI/CD yang terpisah, sehingga pengembangan dan peluncuran fitur dapat dilakukan tanpa mengganggu layanan lain.

* **Edge Computing:** Dengan menggunakan topologi edge, API yang dibangun dengan DDN dapat diakses dengan latensi rendah di seluruh dunia, meningkatkan pengalaman pengguna dan skalabilitas aplikasi.

Arsitektur ini memberikan fleksibilitas dan kecepatan bagi pengembang, memungkinkan mereka untuk membangun dan mengelola aplikasi modern dengan lebih efisien.

### Hasura v2 dan Hasura Data Delivery Network (DDN) v3
merupakan dua versi dari platform Hasura yang berfokus pada kemampuan GraphQL, tetapi ada perbedaan besar dalam arsitektur dan fitur yang disediakan oleh masing-masing versi.

#### **Hasura GraphQL Engine v2:**

* **1. Auto-Generated GraphQL API:** GraphQL API otomatis dari database tanpa perlu menulis kode.
* **2. Real-time Subscriptions:** Mendukung data real-time melalui subscription.
* **3. Role-based Access Control (RBAC):** Kontrol akses berbasis peran untuk keamanan data.
* **4. Remote Schemas:** Integrasi dengan API GraphQL eksternal.
* **5. Actions:** Menambahkan custom business logic melalui HTTP resolvers.
* **6. Event Triggers:** Memicu event berbasis perubahan data di database.
* **7. Remote Joins:** Menggabungkan data dari berbagai sumber (database & API eksternal).
* **8. Custom Business Logic:** Menambahkan logika bisnis dengan SQL functions dan actions.
* **9. Scheduled Triggers:** Menjadwalkan event untuk eksekusi di masa depan.
* **10. Database Migrations:** Otomasi migrasi skema database dengan CLI.
* **11. Monitoring & Observability:** Dukungan observability dengan OpenTelemetry.
* **12. Multi-database Support:** Mendukung beberapa database dalam satu instance.

### **Hasura Data Delivery Network (DDN) v3:**

Hasura DDN v3 adalah langkah maju dari Hasura yang memperkenalkan pendekatan jaringan global untuk mengoptimalkan pengiriman data dari database ke klien.

* **1. Global Data Distribution:** Distribusi data dengan latensi rendah di berbagai lokasi.
* **2. Edge Caching & CDN Integration:** Caching di edge nodes dan integrasi dengan CDN untuk mempercepat pengiriman data.
* **3. Data Routing:** Routing dinamis query ke database atau wilayah yang sesuai.
* **4. Multi-region Replication & Failover:** Replikasi data lintas wilayah dan failover otomatis.
* **5. Intelligent Query Optimization:** Optimasi otomatis untuk performa query yang lebih baik.
* **6. API Rate Limiting:** Pembatasan jumlah query untuk pengguna atau aplikasi.
* **7. Real-time Data Delivery:** Pengiriman data real-time melalui subscription.
* **8. Distributed Event Triggers:** Pemrosesan event triggers secara terdistribusi.
* **9. Edge Data Transformations:** Transformasi data di edge nodes sebelum dikirimkan.
* **10. GraphQL Query Scheduling:** Penjadwalan query untuk eksekusi di masa depan.
* **11. Cross-region Data Joins:** Penggabungan data lintas wilayah dalam satu query.
* **12. Zero Downtime Deployments:** Pembaruan tanpa downtime.
* **13. Multi-cloud & Hybrid Cloud Support:** Dukungan untuk infrastruktur multi-cloud dan hybrid.

### Perbandingan Utama:
**Hasura v2** adalah platform GraphQL yang fokus pada otomatisasi API dengan database relasional seperti Postgres dan MySQL, serta menawarkan fitur seperti RBAC, triggers, dan remote schemas.

**Hasura DDN v3** menambahkan layer distribusi global dan caching untuk mengoptimalkan pengiriman data, meminimalkan latensi, dan mendukung skenario multi-region dengan caching berbasis edge.

### Fitur yang ada dan tidak ada pada V2 dan v3 

**Hasura v2:**

**Fitur yang Ada di v2 tetapi Tidak Ada di v3**

* **1. Scheduled Triggers:** V2 memiliki Scheduled Triggers yang memungkinkan event dijadwalkan untuk dijalankan di masa depan, namun pada DDN v3, fitur ini diakomodasi secara lebih komprehensif melalui query scheduling yang berbeda konteks.

* **2. Database Migrations:** Fitur migrasi database otomatis menggunakan CLI dan mendukung versioning skema adalah bagian integral dari Hasura v2, sementara v3 lebih terfokus pada penyajian data global dan tidak secara langsung menangani migrasi database.

**Hasura DDN v3:** 
**Fitur yang Ada di v3 tetapi Tidak Ada di v2**

**1.Global Data Distribution:**
* Fitur distribusi data global dengan latensi rendah dan distribusi otomatis berdasarkan lokasi pengguna hanya tersedia di v3 (Hasura DDN).

**2.Edge Caching & CDN Integration:**
* V3 mendukung integrasi caching di edge nodes dan CDN untuk meningkatkan kecepatan pengiriman data, tidak tersedia di v2.

**3. Data Routing:**
* Kemampuan routing dinamis query ke database yang berbeda atau wilayah berdasarkan aturan bisnis hanya ada di v3.

**4. Multi-region Replication & Failover:**
* Replikasi data lintas wilayah dan failover otomatis jika terjadi gangguan di satu wilayah hanya ada di v3.

**5. Intelligent Query Optimization:**
* Optimasi query otomatis dengan performa yang ditingkatkan hanya tersedia di v3.

**6. API Rate Limiting:**
* Fitur pembatasan jumlah query yang dapat dilakukan oleh pengguna atau aplikasi ada di v3, tidak tersedia di v2.

**7. Distributed Event Triggers:**
* Pemrosesan event triggers secara terdistribusi di berbagai wilayah hanya ada di v3.

**8. Edge Data Transformations:**
* Transformasi data di edge nodes sebelum dikirimkan ke pengguna hanya ada di v3.

**9. Global-scale Failover and Replication:**
* Fitur failover otomatis dan replikasi global hanya tersedia di v3 untuk memastikan ketersediaan tinggi.

**10. Cross-region Data Joins:**
* Penggabungan data dari berbagai wilayah secara efisien dalam satu query adalah fitur v3.

**11. GraphQL Query Scheduling:**
* V3 mendukung penjadwalan query GraphQL untuk eksekusi di masa depan, fitur ini tidak ada di v2.

**12. Edge Security Features:**
* V3 memiliki keamanan edge seperti enkripsi di edge dan kepatuhan standar keamanan (GDPR, HIPAA, SOC2) yang lebih terfokus dibandingkan v2.

**13. Zero Downtime Deployments:**
* Hasura DDN v3 menjamin tidak ada downtime saat pembaruan, sementara v2 lebih mengandalkan strategi tradisional untuk menangani downtime.

**Hasura GraphQL Engine v2 fokus pada otomatisasi API database, sementara Hasura DDN v3 fokus pada performa global dan pengiriman data cepat.**

### keunggulan dan kekurangan dari Hasura v2 dan Hasura DDN v3:

**Hasura v2:**

**Keunggulan:**

* **Otomatisasi API:** Cepat membuat GraphQL API dari database relasional.
* **Event Triggers:** Bisa memicu webhook berdasarkan perubahan data.
* **Actions & Remote Schemas:** Mendukung logika kustom dan integrasi dengan API lain.
* **Kontrol Akses (RBAC):** Izin akses granular berbasis peran pengguna.
* **Observability:** Integrasi monitoring yang kuat dengan alat seperti Prometheus dan Jaeger.

**Kekurangan:**

* **Tidak ada Caching Global:** Tidak ada caching bawaan untuk mempercepat pengiriman data di seluruh dunia.
* **Tidak ada Edge Computing:** Permintaan pengguna selalu diproses di pusat, sehingga latensi bisa lebih tinggi untuk pengguna global.
* **Kurang optimal untuk multi-region:** Tidak dirancang khusus untuk distribusi data global atau pengiriman lintas wilayah.

**Hasura DDN v3:**

**Keunggulan:**

* **Global Data Caching:** Cache terdistribusi secara global untuk mempercepat pengiriman data.
* **Edge Computing:** Pemrosesan lebih dekat dengan pengguna untuk latensi rendah.
* **Multi-Region Deployment:** Mendukung pengiriman data yang optimal di berbagai wilayah dunia.
* **Skalabilitas & Kinerja:** Sangat cocok untuk aplikasi skala besar dengan pengguna global.
* **Keamanan Tingkat Lanjut:** Mendukung kepatuhan seperti HIPAA dan GDPR.

**Kekurangan:**

* **Kurang fleksibel untuk operasi database spesifik:** Fitur seperti event triggers atau pengelolaan logika database lebih terbatas.
* **Kompleksitas deployment:** Tidak mendukung deployment lokal secara penuh, sehingga lebih cocok untuk aplikasi berbasis cloud.
* **Fokus pada performa global:** Bisa berlebihan untuk aplikasi yang tidak membutuhkan distribusi global.

**Rangkuman:**

* **Hasura v2 unggul dalam otomatisasi API dan fleksibilitas database, tetapi kurang optimal untuk pengiriman data global.**

* **Hasura DDN v3 unggul dalam performa global, dengan caching dan edge computing, tetapi memiliki keterbatasan dalam fitur database spesifik.**
