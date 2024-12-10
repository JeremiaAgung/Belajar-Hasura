#APM

## **APM (Application Performance Monitoring)** 
di Kibana adalah modul yang digunakan untuk memantau kinerja aplikasi secara real-time. Dengan APM, dapat melacak permintaan, latensi, error, dan performa aplikasi secara mendalam, sehingga membantu dalam:

* **Mengidentifikasi Bottleneck**
* 
Dapat melihat bagian mana dari aplikasi yang memperlambat sistem, seperti query lambat, fungsi mahal, atau masalah lain yang memengaruhi performa.

* **Monitoring End-to-End**
* 
APM memungkinkan melacak alur lengkap dari suatu permintaan, mulai dari frontend hingga backend dan database, sehingga Anda memahami perjalanan permintaan secara keseluruhan.

* **Mendeteksi Error**
* 
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

