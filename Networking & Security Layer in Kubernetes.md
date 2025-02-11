# Networking & Security Layer in Kubernetes

## Hubungan dengan API Server
Dalam Kubernetes, komponen **Networking & Security Layer** seperti **CoreDNS, Network Policy, Ingress Controller, dan Service Mesh** berperan dalam komunikasi dan keamanan jaringan. Semua konfigurasi dan operasionalnya dikendalikan oleh **API Server**, yang bertindak sebagai pusat kontrol dalam cluster Kubernetes.

---

## 1. CoreDNS
### **Fungsi**
- CoreDNS adalah **sistem DNS bawaan Kubernetes** yang menangani resolusi nama layanan dalam cluster.
- Mengonversi nama layanan (`myservice.default.svc.cluster.local`) menjadi alamat IP internal pod.

### **Hubungan dengan API Server**
- API Server menyimpan dan mengelola informasi DNS dalam **etcd**.
- CoreDNS membaca perubahan di **etcd** melalui API Server untuk memperbarui resolusi DNS.

### **Analisis API Server pada CoreDNS**
#### **1. Pembahasan Komponen: Pengertian, Fungsi, dan Cara Kerja**
- **Pengertian:** CoreDNS adalah sistem DNS berbasis plugin yang menangani resolusi nama dalam Kubernetes.
- **Fungsi:** Memberikan layanan DNS untuk layanan dan pod dalam cluster.
- **Cara Kerja:** 
  1. API Server menerima perubahan layanan dan pod di Kubernetes.
  2. API Server menyimpan informasi layanan di **etcd**.
  3. CoreDNS membaca data dari **etcd** dan menyediakan resolusi DNS sesuai dengan perubahan yang terjadi.

#### **2. Analisa Dampak Kegagalan Komponen**
- Jika CoreDNS gagal:
  - Resolusi nama layanan akan gagal.
  - Pod tidak dapat berkomunikasi dengan layanan lain menggunakan nama domain.
  - Aplikasi yang bergantung pada DNS (misalnya, microservices) mungkin mengalami kegagalan.

#### **3. Analisis Failure Tolerance**
- Kubernetes memungkinkan menjalankan **multiple CoreDNS pods** untuk redundansi.
- CoreDNS dapat dikonfigurasi dengan **Autoscaling** agar selalu tersedia meskipun ada peningkatan beban.
- Jika salah satu pod CoreDNS gagal, pod lain tetap bisa menangani permintaan DNS.

#### **4. Analisis Single Point of Failure**
- Jika hanya ada satu instance CoreDNS, kegagalan pod akan menyebabkan seluruh layanan DNS dalam cluster terganggu.
- Ketergantungan pada **etcd** juga menjadi faktor risiko; jika **etcd gagal**, CoreDNS tidak dapat memperbarui informasi layanan.

#### **5. Analisis Solusi**
- **Gunakan lebih dari satu instance CoreDNS** dengan **ReplicaSet atau DaemonSet**.
- **Gunakan NodeLocal DNSCache** untuk mengurangi beban CoreDNS.
- **Pantau CoreDNS dengan Prometheus dan Grafana** untuk mendeteksi masalah lebih awal.
- **Pastikan etcd HA (High Availability)** untuk menghindari kegagalan data DNS.

---

## 2. Network Policy
### **Fungsi**
- Network Policy mengontrol lalu lintas jaringan antar pod berdasarkan aturan keamanan yang ditentukan.
- Menggunakan **CNI Plugin** (misalnya, Calico, Cilium) untuk menerapkan kebijakan keamanan jaringan.

### **Hubungan dengan API Server**
- API Server menerima, menyimpan, dan mengelola objek **NetworkPolicy** dalam etcd.
- Network Plugin membaca kebijakan dari API Server untuk menerapkannya di jaringan pod.

### **Analisis API Server pada Network Policy**
#### **1. Pembahasan Komponen: Pengertian, Fungsi, dan Cara Kerja**
- **Pengertian:** Network Policy adalah fitur Kubernetes yang memungkinkan administrator mengontrol lalu lintas jaringan antar pod berdasarkan aturan yang telah ditentukan.
- **Fungsi:** Membantu meningkatkan keamanan jaringan dengan membatasi komunikasi antar pod berdasarkan namespace, label, dan aturan protokol tertentu.
- **Cara Kerja:**
  1. Administrator mendefinisikan aturan Network Policy dalam bentuk **YAML manifest**.
  2. API Server menyimpan dan mengelola aturan tersebut dalam **etcd**.
  3. CNI Plugin (Calico, Cilium, dll.) membaca aturan dari API Server dan menerapkannya ke jaringan pod.

#### **2. Analisa Dampak Kegagalan Komponen**
- Jika Network Policy gagal:
  - Semua pod mungkin bisa saling berkomunikasi tanpa batasan keamanan.
  - Pod yang seharusnya tidak memiliki akses ke layanan tertentu bisa mendapatkan akses, meningkatkan risiko serangan keamanan.
  - Jika Network Plugin gagal membaca kebijakan dari API Server, perubahan kebijakan tidak akan diterapkan.

#### **3. Analisis Failure Tolerance**
- Kubernetes memungkinkan **multi-node deployment** dari Network Policy Plugin untuk redundansi.
- CNI Plugin yang mendukung HA (seperti Calico dan Cilium) dapat memastikan bahwa kebijakan tetap diterapkan meskipun ada kegagalan sebagian.
- Network Policy bersifat **declarative**, sehingga jika API Server kembali normal, aturan akan tetap diterapkan sesuai konfigurasi yang ada.

#### **4. Analisis Single Point of Failure**
- Jika API Server gagal, tidak ada perubahan kebijakan baru yang dapat diterapkan.
- Jika **etcd** gagal, Network Policy tidak dapat diambil atau diperbarui.
- Jika hanya ada satu instance CNI Plugin, kegagalan pada plugin dapat menyebabkan kebijakan tidak diterapkan atau terjadi konektivitas yang tidak diinginkan.

#### **5. Analisis Solusi**
- **Gunakan lebih dari satu instance API Server** dengan mode **HA (High Availability)**.
- **Gunakan CNI Plugin yang mendukung failover**, seperti Calico dengan mode HA atau Cilium.
- **Pantau Network Policy dengan tools seperti Cilium Hubble** untuk mendeteksi anomali lalu lintas jaringan.
- **Simpan cadangan konfigurasi Network Policy** agar dapat diterapkan ulang jika terjadi kegagalan.

---

## 3. Ingress Controller
### **Fungsi**
- Mengelola akses HTTP/HTTPS dari luar ke dalam cluster Kubernetes.
- Menggunakan aturan **Ingress** untuk mengarahkan traffic ke layanan yang tepat.

### **Hubungan dengan API Server**
- API Server menerima dan menyimpan objek **Ingress** di **etcd**.
- Ingress Controller membaca konfigurasi dari API Server untuk mengatur routing traffic.

### **Dampak jika Ingress Controller gagal**
- Aplikasi dalam cluster tidak dapat diakses dari luar.
- API Server tidak terpengaruh secara langsung, tetapi pengguna mungkin tidak dapat mengakses layanan berbasis web.

### **Solusi**
- Menjalankan **Ingress Controller dalam mode HA**.
- Menggunakan Load Balancer eksternal untuk meningkatkan ketersediaan.

---

## 4. Service Mesh (Istio, Linkerd)
### **Fungsi**
- Menyediakan fitur **security, observability, dan traffic management** untuk komunikasi antar layanan dalam cluster.
- Menggunakan **sidecar proxy** untuk mengontrol dan memantau lalu lintas antar pod.

### **Hubungan dengan API Server**
- API Server menyimpan konfigurasi **Service Mesh** dalam Custom Resource Definitions (CRD).
- Control Plane (misalnya Istio Pilot) membaca CRD dari API Server untuk mengatur lalu lintas dan keamanan layanan.

### **Dampak jika Service Mesh gagal**
- Komunikasi antar layanan bisa terganggu atau mengalami latensi tinggi.
- API Server tetap berjalan, tetapi observability dan security enforcement bisa terpengaruh.

### **Solusi**
- Menjalankan **multi-instance control plane** untuk memastikan HA.
- Menggunakan monitoring tools seperti **Kiali** untuk Istio.

---

## Kesimpulan
| **Komponen**         | **Peran dalam Networking & Security** | **Hubungan dengan API Server** |
|----------------------|--------------------------------|--------------------------------|
| **CoreDNS**         | Resolusi DNS internal pod & layanan | API Server menyimpan info DNS di etcd, CoreDNS membacanya untuk resolusi |
| **Network Policy**  | Mengontrol lalu lintas antar pod | API Server menyimpan aturan keamanan jaringan di etcd |
| **Ingress Controller** | Mengelola akses HTTP/HTTPS dari luar ke dalam cluster | API Server menyimpan dan mengelola konfigurasi Ingress |
| **Service Mesh**    | Observability, security, dan traffic management antar layanan | API Server menyimpan konfigurasi CRD untuk Service Mesh |

Semua komponen ini bergantung pada **API Server** untuk konfigurasi dan operasionalnya. Jika **API Server gagal**, maka sistem networking & security dalam Kubernetes bisa terganggu. Oleh karena itu, **High Availability (HA), monitoring, dan backup** sangat penting untuk memastikan kestabilan cluster Kubernetes. 🚀
