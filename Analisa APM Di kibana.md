# APMM

## **APM (Application Performance Monitoring)** 
di Kibana adalah modul yang digunakan untuk memantau kinerja aplikasi secara real-time. Dengan APM, dapat melacak permintaan, latensi, error, dan performa aplikasi secara mendalam, sehingga membantu dalam:

**Mengidentifikasi Bottleneck** Dapat melihat bagian mana dari aplikasi yang memperlambat sistem, seperti query lambat, fungsi mahal, atau masalah lain yang memengaruhi performa.

**Monitoring End-to-End** APM memungkinkan melacak alur lengkap dari suatu permintaan, mulai dari frontend hingga backend dan database, sehingga memahami perjalanan permintaan secara keseluruhan.

**Mendeteksi Error** dapat menangkap error atau exception yang terjadi di aplikasi dan melihat trace-nya untuk memahami akar penyebabnya.

## **Cara Kerja APM di Kibana**

**Agent**

perlu menginstal APM Agent di aplikasi. Agent ini tersedia untuk berbagai bahasa pemrograman seperti Node.js, Java, Python, dan lain-lain. Agent mengumpulkan data terkait permintaan, error, dan performa.

**APM Server**

Agent mengirimkan data ke APM Server, yang merupakan bagian dari Elastic Stack. APM Server memproses data sebelum menyimpannya ke Elasticsearch.

**Kibana APM UI**

Data yang sudah disimpan di Elasticsearch ditampilkan melalui Kibana dalam bentuk grafik, heatmap, dan trace untuk membantu analisis lebih mudah.

## **Fitur Utama APM di Kibana**

**Transaction Monitoring:** Melihat performa berbagai transaksi aplikasi.

**Service Map:** Visualisasi hubungan antar layanan di aplikasi.

**Trace:** Melihat detail langkah-langkah yang diambil suatu permintaan.

**Error Monitoring:** Laporan error beserta konteksnya.

**Metrics:** Memonitor metrik sistem seperti CPU dan memori.


Berikut Adalah analisan dari APM
`http://10.100.13.25:5601/app/apm/services/hasura/transactions/`

![image](https://github.com/user-attachments/assets/fdcd6db0-1839-41d1-9be7-762a6a8b3629)

Gambar menunjukkan grafik dari APM (Application Performance Monitoring) di Kibana untuk endpoint /v1/graphql di Hasura. 

Berikut adalah penjelasan dari masing-masing metrik yang ditampilkan:

### **1. Latency**

* **Grafik kiri (Latency):**
Menunjukkan waktu rata-rata (Average Latency) yang dibutuhkan oleh endpoint /v1/graphql untuk memproses permintaan (dalam milidetik).
Lonjakan (spike) di awal menunjukkan waktu latensi yang lebih tinggi dari biasanya, yang mungkin terjadi karena beban awal atau kueri kompleks.
Grafik turun menunjukkan waktu latensi kembali ke angka yang lebih rendah, yang idealnya menandakan bahwa performa sistem membaik setelah beban tinggi selesai.

### **2. Throughput**

* **Grafik kanan (Throughput):**
Menunjukkan jumlah permintaan (Requests Per Minute - RPM atau TPM) yang diproses oleh endpoint /v1/graphql dalam satu menit. Lonjakan throughput pada titik tertentu menunjukkan bahwa sistem sedang menangani lebih banyak kueri atau beban. Penurunan throughput biasanya mengindikasikan berkurangnya jumlah permintaan ke endpoint tersebut. Interpretasi Data Ketika throughput tinggi tetapi latensi tetap rendah, itu menunjukkan bahwa sistem dapat menangani beban dengan efisien. Jika latensi meningkat bersamaan dengan throughput tinggi, mungkin ada
masalah performa seperti: Query GraphQL terlalu kompleks, Beban sistem (CPU atau memori) mendekati batasnya, Bottleneck di database backend.

Dalam grafik ini, terlihat bahwa lonjakan throughput tidak selalu diiringi oleh kenaikan latensi yang signifikan, yang artinya performa Hasura cukup stabil meskipun ada peningkatan beban.

### **Kesimpulan**

**Optimasi performa:** Identifikasi lonjakan latensi untuk melihat apakah ada kueri atau pengguna yang membebani sistem.

**Monitoring beban:** Perhatikan throughput untuk mengetahui kapan waktu penggunaan tertinggi.

**Debugging:** Gunakan insight ini untuk menelusuri masalah pada waktu tertentu menggunakan log atau tracing dari APM.

### **Failed transaction rate**

![image](https://github.com/user-attachments/assets/a865846f-8675-4643-bf1b-64f7f1a0df92)

Penjelasan:

Dari grafik, dapat dilihat bahwa tingkat kegagalan transaksi mendekati 0% selama periode waktu tersebut. Ini mengindikasikan bahwa aplikasi berjalan dengan baik tanpa banyak transaksi yang gagal.

### **Traces Samples**

![image](https://github.com/user-attachments/assets/12de1735-f4c6-42a8-ae9d-4a42d584ed3a)

Gambar ini adalah tampilan dari trace di APM Kibana untuk endpoint /v1/graphql pada Hasura. Berikut adalah penjelasan rinci mengenai data yang ditampilkan:

**1. Latency Distribution**

* **Histogram Latency:**
Grafik ini menunjukkan distribusi latensi dari total 19.250 transaksi. Sumbu X menunjukkan waktu latensi (dalam milidetik), dan sumbu Y menunjukkan jumlah transaksi pada rentang waktu tertentu. Distribusi yang lebih tinggi di sisi kiri menunjukkan bahwa mayoritas transaksi selesai dalam waktu latensi rendah (0–100 ms). 
95p: Titik persentil ke-95 menunjukkan bahwa 95% dari transaksi selesai dalam waktu sekitar rentang ini. Ini merupakan metrik penting untuk memantau performa aplikasi.

### **Timeline**

![image](https://github.com/user-attachments/assets/775ebe71-63e2-4596-ba0b-a72387e58f42)

**Timeline**
/v1/graphql (4.3 ms): Total waktu yang diperlukan untuk menyelesaikan satu permintaan adalah 4.3 ms.
Ini termasuk semua langkah di bawahnya seperti parsing, eksekusi query, dan interaksi dengan backend.

**Parse GraphQL (55 µs):
Waktu yang dihabiskan untuk mem-parse kueri GraphQL yang diterima. Ini adalah langkah awal untuk memahami kueri sebelum mengeksekusinya. 

**Resolve Query Execution Plan (188 µs):**
Proses menyusun rencana eksekusi kueri. Dalam konteks ini, Hasura menentukan bagaimana kueri akan diterjemahkan ke query SQL ke database.

**Parse Query (81 µs):**
Langkah parsing untuk menyiapkan query SQL yang akan dikirim ke backend database. 

**Resolve Execution Step for "transaks1" (58 µs):**
Menunjukkan langkah-langkah spesifik dalam eksekusi kueri untuk entitas atau tabel bernama transaks1.

**Data Connector Backend Query (3.7 ms):**
Waktu yang dibutuhkan untuk berkomunikasi dengan backend database (misalnya MySQL). Terlihat bahwa sebagian besar waktu dihabiskan pada langkah ini, karena menghubungkan dengan database sering menjadi bottleneck.

**QueryResponse Reshaping (34 µs):**
Proses mengubah data yang diterima dari backend agar sesuai dengan format respon GraphQL. Proses ini sangat cepat dan tidak signifikan dalam total waktu.

**Process Remote Joins (1 µs):**
Jika ada relasi lintas sumber data (remote joins), langkah ini akan menangani mereka. Dalam kasus ini, langkah ini hampir tidak memakan waktu.


