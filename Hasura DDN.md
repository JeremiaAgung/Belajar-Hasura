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

#### **Hasura v2:**

**1.GraphQL API:**

* Fokus utama Hasura v2 adalah mengotomatisasi pembuatan GraphQL API berbasis database relasional, seperti PostgreSQL dan MySQL. Setiap perubahan pada database (seperti penambahan tabel atau kolom) secara otomatis menghasilkan endpoint GraphQL yang sesuai.

**2.Remote Schemas & Actions:**

* Pada Hasura v2, Anda dapat menghubungkan remote schemas untuk menggabungkan berbagai sumber GraphQL ke dalam satu endpoint.
Actions juga ditambahkan untuk memungkinkan penanganan logika kustom (custom business logic) yang tidak hanya terbatas pada operasi CRUD.

**3.Event Triggers:**

* Mendukung event triggers, memungkinkan pengguna untuk mendefinisikan peristiwa berbasis database (misalnya, insert atau update) yang kemudian dapat memicu webhook eksternal atau menjalankan fungsi serverless.

**4.Role-Based Access Control (RBAC):**

* Memungkinkan pengguna untuk mendefinisikan izin berdasarkan role, sehingga setiap query dan mutation GraphQL dibatasi berdasarkan siapa yang mengaksesnya.

**5.Konektivitas dengan Postgres:**

* Di Hasura v2, PostgreSQL tetap menjadi database inti, dengan MySQL ditambahkan sebagai database sekunder dalam beberapa versi.

**6.Deployment & Monitoring:**

* Hasura v2 memungkinkan pengguna untuk mendesain aplikasi dengan men-deploy di cloud maupun on-premise, serta bisa diintegrasikan dengan observability tools seperti Prometheus dan Jaeger.

### **Hasura Data Delivery Network (DDN) v3:**

Hasura DDN v3 adalah langkah maju dari Hasura yang memperkenalkan pendekatan jaringan global untuk mengoptimalkan pengiriman data dari database ke klien.

**1.Global Data Distribution:**

* DDN adalah jaringan global yang memungkinkan pengiriman data yang lebih cepat dan optimal dari lokasi database ke klien. Fokusnya adalah untuk meminimalkan latensi dengan mendistribusikan permintaan secara cerdas berdasarkan lokasi pengguna.

**2.Caching Layer:**

* Salah satu fitur penting dari DDN adalah caching yang terdistribusi secara global. Permintaan GraphQL yang sering digunakan akan di-cache untuk mempercepat pengiriman data, sehingga mengurangi beban pada database dan server pusat.

**3.Multi-Region Deployment:**

* DDN mendukung multi-region deployments, memungkinkan pengiriman data lintas wilayah dengan latensi yang sangat rendah. Hal ini sangat penting untuk aplikasi global yang melayani pengguna di berbagai belahan dunia.

**4.Edge Computing:**

* Hasura DDN v3 menggunakan edge computing untuk memproses permintaan lebih dekat ke lokasi pengguna, mengurangi waktu perjalanan data dari klien ke server, dan mengurangi latensi.

**5.Scaling & Reliability:**

* Dengan DDN, Hasura menjadi lebih andal dan terukur dalam hal kinerja dan uptime, karena menggunakan infrastruktur jaringan global untuk mendistribusikan beban permintaan.

**6.Advanced Security & Compliance:**

* DDN v3 juga memberikan tingkat keamanan dan kepatuhan yang lebih tinggi, yang dirancang untuk memenuhi persyaratan industri seperti HIPAA, GDPR, dan lainnya.
