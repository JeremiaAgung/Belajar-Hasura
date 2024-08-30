# KUBERNETES(K8s)

Kubernetes, sering disingkat sebagai k8s, adalah sebuah platform open-source yang dirancang untuk mengotomatisasi proses deployment, scaling, dan manajemen aplikasi yang terkontainerisasi. 

### 1. Kubernetes (K8s)

### Kelebihan:
**Otomatisasi:** Kubernetes otomatis mengelola penempatan (placement) kontainer di node yang tepat berdasarkan kebutuhan sumber daya.

**Scalability:** Dapat dengan mudah menyesuaikan skala aplikasi, baik secara manual maupun otomatis berdasarkan metrik tertentu.

**Load Balancing & Service Discovery:** Mengelola dan mendistribusikan lalu lintas ke pod yang tepat tanpa memerlukan pengaturan manual.

**Self-healing:** Secara otomatis memulai kembali kontainer yang gagal, menggantikan, atau memindahkan kontainer saat node mati.

**Rolling Updates & Rollbacks:** Mendukung pembaruan aplikasi secara bertahap tanpa downtime, dan memudahkan rollback jika terjadi kesalahan.

### Kekurangan:
**Kompleksitas:** Setup dan manajemen Kubernetes dapat menjadi rumit, terutama bagi pemula.

**Overhead Sumber Daya:** Menjalankan Kubernetes memerlukan sumber daya yang signifikan, terutama pada cluster yang besar.

**Keamanan:** Karena sifatnya yang terdistribusi, Kubernetes memerlukan pendekatan keamanan yang komprehensif dan terpusat.

**Pemeliharaan:** Membutuhkan tim yang terlatih dan berpengalaman untuk memelihara dan mengelola cluster secara efektif.

### 2. Networking di Kubernetes
Kubernetes mengimplementasikan model jaringan yang cukup kompleks untuk memastikan komunikasi yang lancar antara berbagai komponen (pod, service, etc.).

**Pod Network:** Setiap pod dalam Kubernetes diberi alamat IP unik, memungkinkan pod untuk berkomunikasi satu sama lain tanpa perlu NAT (Network Address Translation).

**Service Network:** Menggunakan objek Service, Kubernetes menyediakan mekanisme load balancing untuk mendistribusikan traffic ke pod yang sesuai.

**Ingress:** Ingress mengatur akses dari luar ke dalam cluster, seperti HTTP/S traffic. Dapat mengelola routing, TLS termination, dan lebih banyak lagi.

**Network Policies:** Mengontrol lalu lintas jaringan pada level pod, memungkinkan aturan granular untuk komunikasi yang lebih aman.

### kelebihan

Isolasi jaringan yang baik antara berbagai aplikasi dalam cluster.

Mendukung load balancing internal dan eksternal secara otomatis.

Memiliki mekanisme yang terdefinisi dengan baik untuk mengelola akses dari luar (Ingress).

### Kekurangan 

Setup dan troubleshooting networking di Kubernetes bisa kompleks, terutama pada cluster yang besar dan heterogen.

Ketergantungan pada plugin jaringan pihak ketiga untuk beberapa fitur.

### 3. Volume di Kubernetes

**Volume di Kubernetes** adalah cara untuk menyimpan data yang dapat bertahan (persistent storage) dan dapat diakses oleh pod yang berjalan.

**Ephemeral Volume:** Volume ini ada hanya selama pod berjalan.

**PersistentVolume (PV) dan PersistentVolumeClaim (PVC):** PersistentVolume adalah unit penyimpanan di cluster yang dapat dimanfaatkan oleh pod. 

**ersistentVolumeClaim** adalah klaim dari PV oleh pengguna untuk digunakan pada pod mereka.

**Storage Classes:** Menyediakan cara dinamis untuk menyediakan PV berdasarkan kebutuhan penyimpanan yang berbeda, seperti SSD atau HDD.

### Kelebihan:

Memungkinkan penyimpanan data yang persisten di luar lifecycle pod.

Mendukung berbagai jenis penyimpanan, termasuk NFS, iSCSI, dan cloud storage.

Memiliki fitur snapshot dan clone untuk pemulihan data yang lebih mudah.

### Kekurangan:

Setup persistent storage bisa rumit, terutama di lingkungan on-premise.

Berbagai tipe volume mungkin memerlukan plugin atau konfigurasi tambahan.

