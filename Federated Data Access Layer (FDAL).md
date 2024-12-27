# Federated Data Access Layer (FDAL) dan Supergraph Platform

## 1. Pengertian Federated Data Access Layer (FDAL)

**FDAL (Federated Data Access Layer)** adalah suatu lapisan yang memungkinkan akses yang fleksibel dan aman ke berbagai sumber data yang dikelola secara independen. Artinya, FDAL mengintegrasikan berbagai sumber data yang terpisah, seperti basis data atau layanan API yang berbeda, ke dalam satu lapisan tunggal, tanpa memerlukan penggabungan fisik atau pemindahan data.

FDAL memberikan kemampuan untuk mengakses data dari beberapa sumber yang berbeda secara terpadu. Data ini bisa berasal dari berbagai sistem yang mungkin memiliki aturan pengelolaan atau struktur data yang berbeda.

### Tujuan Utama FDAL:
- Menyediakan satu titik akses yang konsisten dan efisien meskipun sumber data yang dikelola secara terpisah.
  
### Typical Consumers (Konsumen FDAL):
Konsumen FDAL adalah berbagai aplikasi atau sistem yang membutuhkan akses ke data, antara lain:
- **Low-latency, high-concurrency access to realtime data**: Aplikasi yang memantau dan menganalisis data secara real-time.
- **Access to analytical data**: Data yang digunakan untuk analisis, laporan, dan wawasan berbasis data historis.
- **Experience Layer Products & Microservices**: Layanan mikro yang mengkonsumsi FDAL, seperti BFFs (Backend for Frontends).
- **Internal Products & Services (Reporting, BI, etc.)**: Sistem internal yang digunakan untuk laporan dan analitik.
- **3rd Party Developers**: Pengembang pihak ketiga yang membutuhkan akses ke data untuk aplikasi mereka.
- **Emerging Use Cases**: Aplikasi AI dan model besar yang membutuhkan akses ke data besar atau terdiversifikasi.

### Manfaat FDAL:
- **Mengurangi biaya dan meningkatkan efisiensi**: Menghindari pemindahan data yang tidak perlu antar platform dan mengurangi kompleksitas.
- **Meningkatkan kepatuhan dan tata kelola**: Penerapan model otorisasi yang konsisten.
- **Akses data real-time**: Memungkinkan keputusan berbasis data yang cepat.
- **Meningkatkan produktivitas dan kolaborasi**: Menyediakan API yang stabil dan mendukung logika bisnis lintas domain.
- **Mengakomodasi dinamika pasar**: Memfasilitasi kolaborasi antara produsen dan konsumen data.

---

## 2. Checklist untuk Membangun Supergraph Platform dengan FDAL

### I. Unified Semantic Model (Model Semantik Terpadu)
**Tujuan**: Memahami berbagai entitas dalam supergraph seperti sumber daya, metode bisnis, dan kebijakan otorisasi.
- **Penjelasan**: Model semantik bertindak sebagai bahasa umum yang menghubungkan berbagai domain data dan memberikan makna yang konsisten di seluruh supergraph.

### II. Data Modeling & Business Logic (Pemodelan Data & Logika Bisnis)
**Tujuan**: Subgraph connectors harus memungkinkan pemodelan domain atau API menggunakan bahasa dari sumber data yang mendasarinya, serta menambahkan logika bisnis untuk transformasi, validasi, dan otorisasi.
- **Penjelasan**: Subgraph harus cukup "tipis" untuk memaksimalkan performa, namun cukup "tebal" untuk menyertakan logika bisnis yang diperlukan.

### III. Authorization (Otorisasi)
**Tujuan**: Mendukung kebijakan otorisasi, termasuk:
- Komposisi aturan/policy
- Pengaturan akses tingkat kolom dan entitas
- Integrasi yang dioptimalkan dengan pengambilan data
- **Penjelasan**: Sistem harus mengatur siapa yang dapat mengakses data pada tingkat yang sangat rinci, serta mengontrol akses berdasarkan aturan dan kebijakan.

### IV. API Design (Desain API)
**Tujuan**: Menyediakan API untuk menangani kebutuhan domain-driven dan menyediakan operasi untuk query dan invoke business methods.
- **Penjelasan**:
  - Menyediakan cara untuk query data dan invoke business methods.
  - Menangani operasi seperti filtering, sorting, pagination, dan aggregation.
  - Menangani berbagai jenis data (relasional, event-driven, key-value, dan graph).
  - Menyediakan API untuk agregasi dan orkestrasi lintas domain.

### V. Performance & Observability (Kinerja & Pengamatan)
**Tujuan**: Memastikan sistem memiliki kemampuan untuk:
- **Query planning**: Memahami bagaimana query dijalankan.
- **Tracing**: Memantau jalannya query di produksi.
- **Optimisasi data-source**: Mengoptimalkan cara pengambilan data.
- **Latency tax**: Memahami dan mengoptimalkan peningkatan latensi akibat lapisan tambahan.

### VI. Federated Ownership (Kepemilikan Terfederasi)
**Tujuan**: Memungkinkan tim yang berbeda bekerja secara independen pada domain mereka masing-masing dengan CI/CD yang terpisah.
- **Penjelasan**:
  - **Composability**: Memungkinkan subgraph digabungkan dari berbagai domain.
  - **Analytics & Collaboration**: Alat analitik dan kolaborasi untuk pengelola dan konsumen data.

---

## Kesimpulan

Secara keseluruhan, FDAL memungkinkan berbagai jenis pengguna atau aplikasi untuk mengakses data yang tersebar di banyak sistem atau sumber data tanpa perlu mengetahui detail teknis tentang bagaimana data tersebut disimpan atau dikelola. Dengan menggabungkan berbagai komponen dalam supergraph, platform ini menyediakan fleksibilitas, skalabilitas, dan keamanan dalam pengelolaan data yang terdistribusi.
