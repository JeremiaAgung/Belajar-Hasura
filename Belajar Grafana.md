# GRAFANA
Grafana terhubung ke Prometheus untuk visualisasi data metrics. Anda dapat membuat dashboard dan grafik menggunakan query PromQL untuk memantau aplikasi atau infrastruktur secara real-time, termasuk alerting berbasis metrics.

Pada Bagian Overview panel terdapat 7 dashborad  
![image](https://github.com/user-attachments/assets/67adbd98-57ba-4cd8-91ee-dfff17423822)

tampilan dashboard Grafana yang menunjukkan metrics terkait Hasura HTTP GraphQL, yang diambil dari data Prometheus.

* **Total Queries**: Menampilkan 48 query yang telah dijalankan.
* **Query Latency (P95)**: Waktu latensi untuk 95% dari query adalah 28,8 ms.
* **Total Mutations**: Ada 1 operasi mutasi yang telah dilakukan.
* **Mutation Latency (P95)**: Latensi mutasi (P95) adalah 9,50 ms.
* **Top Queries dan Top Mutations**: Tidak ada data spesifik yang ditampilkan di bagian ini selain servis `hasuraferdy` yang terdaftar.

Grafana memvisualisasikan data ini untuk memantau performa dan responsivitas Hasura.

