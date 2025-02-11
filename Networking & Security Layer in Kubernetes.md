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

### **Dampak jika CoreDNS gagal**
- Pod tidak dapat menyelesaikan nama layanan internal.
- API Server tetap berjalan, tetapi aplikasi mungkin mengalami kegagalan komunikasi.

### **Solusi**
- Menjalankan **multiple CoreDNS replicas** untuk High Availability (HA).
- Menggunakan **NodeLocal DNSCache** untuk meningkatkan kinerja DNS.

---

## 2. Network Policy
### **Fungsi**
- Network Policy mengontrol lalu lintas jaringan antar pod berdasarkan aturan keamanan yang ditentukan.
- Menggunakan **CNI Plugin** (misalnya, Calico, Cilium) untuk menerapkan kebijakan keamanan jaringan.

### **Hubungan dengan API Server**
- API Server menerima, menyimpan, dan mengelola objek **NetworkPolicy** dalam etcd.
- Network Plugin membaca kebijakan dari API Server untuk menerapkannya di jaringan pod.

### **Dampak jika Network Policy gagal**
- Potensi gangguan keamanan jika akses tidak dibatasi dengan benar.
- Pod bisa kehilangan konektivitas ke layanan penting seperti API Server, CoreDNS, atau database.

### **Solusi**
- Validasi **Network Policy** sebelum diterapkan (`kubectl describe networkpolicy`).
- Monitoring kebijakan jaringan menggunakan tools seperti **Cilium Hubble**.

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
