# KUBERNETES(K8s)

Kubernetes, sering disingkat sebagai k8s, adalah sebuah platform open-source yang dirancang untuk mengotomatisasi proses deployment, scaling, dan manajemen aplikasi yang terkontainerisasi. 

### 1. Kubernetes (K8s)

### Kelebihan:
**-Otomatisasi:** Kubernetes otomatis mengelola penempatan (placement) kontainer di node yang tepat berdasarkan kebutuhan sumber daya.

**-Scalability:** Dapat dengan mudah menyesuaikan skala aplikasi, baik secara manual maupun otomatis berdasarkan metrik tertentu.

**-Load Balancing & Service Discovery:** Mengelola dan mendistribusikan lalu lintas ke pod yang tepat tanpa memerlukan pengaturan manual.

**-Self-healing:** Secara otomatis memulai kembali kontainer yang gagal, menggantikan, atau memindahkan kontainer saat node mati.

**-Rolling Updates & Rollbacks:** Mendukung pembaruan aplikasi secara bertahap tanpa downtime, dan memudahkan rollback jika terjadi kesalahan.

### Kekurangan:
**-Kompleksitas:** Setup dan manajemen Kubernetes dapat menjadi rumit, terutama bagi pemula.

**-Overhead Sumber Daya:** Menjalankan Kubernetes memerlukan sumber daya yang signifikan, terutama pada cluster yang besar.

**-Keamanan:** Karena sifatnya yang terdistribusi, Kubernetes memerlukan pendekatan keamanan yang komprehensif dan terpusat.

**-Pemeliharaan:** Membutuhkan tim yang terlatih dan berpengalaman untuk memelihara dan mengelola cluster secara efektif.

### 2. Networking di Kubernetes
Kubernetes mengimplementasikan model jaringan yang cukup kompleks untuk memastikan komunikasi yang lancar antara berbagai komponen (pod, service, etc.).

**-Pod Network:** Setiap pod dalam Kubernetes diberi alamat IP unik, memungkinkan pod untuk berkomunikasi satu sama lain tanpa perlu NAT (Network Address Translation).

**-Service Network:** Menggunakan objek Service, Kubernetes menyediakan mekanisme load balancing untuk mendistribusikan traffic ke pod yang sesuai.

**-Ingress:** Ingress mengatur akses dari luar ke dalam cluster, seperti HTTP/S traffic. Dapat mengelola routing, TLS termination, dan lebih banyak lagi.

**-Network Policies:** Mengontrol lalu lintas jaringan pada level pod, memungkinkan aturan granular untuk komunikasi yang lebih aman.

### kelebihan

Isolasi jaringan yang baik antara berbagai aplikasi dalam cluster.

Mendukung load balancing internal dan eksternal secara otomatis.

Memiliki mekanisme yang terdefinisi dengan baik untuk mengelola akses dari luar (Ingress).

### Kekurangan 

Setup dan troubleshooting networking di Kubernetes bisa kompleks, terutama pada cluster yang besar dan heterogen.

Ketergantungan pada plugin jaringan pihak ketiga untuk beberapa fitur.

### 3. Volume di Kubernetes

**-Volume di Kubernetes** adalah cara untuk menyimpan data yang dapat bertahan (persistent storage) dan dapat diakses oleh pod yang berjalan.

**-Ephemeral Volume:** Volume ini ada hanya selama pod berjalan.

**-PersistentVolume (PV) dan PersistentVolumeClaim (PVC):** PersistentVolume adalah unit penyimpanan di cluster yang dapat dimanfaatkan oleh pod. 

**-ersistentVolumeClaim** adalah klaim dari PV oleh pengguna untuk digunakan pada pod mereka.

**-Storage Classes:** Menyediakan cara dinamis untuk menyediakan PV berdasarkan kebutuhan penyimpanan yang berbeda, seperti SSD atau HDD.

### Kelebihan:

Memungkinkan penyimpanan data yang persisten di luar lifecycle pod.

Mendukung berbagai jenis penyimpanan, termasuk NFS, iSCSI, dan cloud storage.

Memiliki fitur snapshot dan clone untuk pemulihan data yang lebih mudah.

### Kekurangan:

Setup persistent storage bisa rumit, terutama di lingkungan on-premise.

Berbagai tipe volume mungkin memerlukan plugin atau konfigurasi tambahan.

### Command-Command Kubernetes

Berikut adalah beberapa command dasar yang sering digunakan dalam Kubernetes:

**a. Membuat Deployment**

```
kubectl create deployment [nama-deployment] --image=[nama-image]
```
contoh

```
kubectl create deployment nginx-deployment --image=nginx
```

**b. Mengelola Pods**

Melihat Pods yang Berjalan:

```
kubectl get pods

```

Menghapus Pod:

```
kubectl delete pod [nama-pod]
```
**c. Mengelola Services**

Membuat Service:

```
kubectl expose deployment [nama-deployment] --type=[tipe-service] --port=[port]
```

**d.Melihat Logs Pod:**

```
kubectl logs [nama-pod]
```

**e. Mengganti Context Cluster**

```
kubectl config use-context [nama-context]
```

**f. Melakukan Scaling pada Deployment**

```
kubectl scale deployment [nama-deployment] --replicas=[jumlah-replicas]
```
contoh

```
kubectl scale deployment nginx-deployment --replicas=3
```

### Apa itu Kubelet?
**Kubelet** adalah komponen penting dalam arsitektur Kubernetes yang berjalan pada setiap node dalam cluster. Fungsinya adalah untuk:

-Mengambil instruksi dari control plane (melalui API server) dan menjalankan container yang ditentukan dalam Pod di node tersebut.

-Memastikan bahwa container yang didefinisikan dalam Pod tetap berjalan dan sehat.

-Melakukan monitoring pada resource yang digunakan oleh container di node tersebut.

**Arsitektur:**

**-Node:** Di dalam setiap node Kubernetes, terdapat Kubelet yang bertugas berkomunikasi dengan API server di control plane.

**-Pods:** Kubelet bertanggung jawab untuk menjalankan Pods di dalam node tersebut.

**-Container Runtime:** Kubelet berinteraksi dengan container runtime (seperti Docker atau containerd) untuk menjalankan container sesuai dengan spesifikasi yang diberikan oleh control plane.

### Berikut adalah beberapa contoh command yang dapat dijalankan dengan `kubelet`:

**1. Menjalankan `kubelet` dengan parameter default:**
```
kubelet --config=/var/lib/kubelet/config.yaml
```

**2. Menentukan runtime container:**
Jika menggunakan `containerd` sebagai container runtime, bisa mengatur dengan command berikut:
```
kubelet --container-runtime=remote --container-runtime-endpoint=unix:///run/containerd/containerd.sock

```

**3.Mengatur file konfigurasi Kubelet:**
dapat menggunakan flag `--config` untuk menunjuk ke file konfigurasi YAML yang memuat semua pengaturan Kubelet.
```
kubelet --config=/etc/kubernetes/kubelet-config.yaml
```
**4.Menentukan direktori untuk pod-manifest:**
Untuk menjalankan pod statis, Anda dapat menggunakan flag `--pod-manifest-path`:
```
kubelet --pod-manifest-path=/etc/kubernetes/manifests
```
**5.Menentukan server API Kubernetes:**
Untuk menghubungkan kubelet ke API server, gunakan flag `--kubeconfig`:
```
kubelet --kubeconfig=/etc/kubernetes/kubelet.kubeconfig
```
**6.Menentukan Node IP secara manual:**
Jika node memiliki lebih dari satu interface jaringan, Anda bisa menetapkan IP node secara manual:
```
kubelet --node-ip=192.168.1.100
```
**7.Mengaktifkan fitur tertentu:**
Misalnya, untuk mengaktifkan fitur alpha tertentu, gunakan flag `--feature-gates`:
```
kubelet --feature-gates=SomeAlphaFeature=true
```

**8.Menentukan jaringan plugin:**
Jika Anda menggunakan plugin jaringan seperti CNI, Anda dapat mengatur plugin tersebut dengan flag `--network-plugin`:
```
kubelet --network-plugin=cni --cni-conf-dir=/etc/cni/net.d --cni-bin-dir=/opt/cni/bin
```

### Apa itu kubeadm?
**Kubeadm** adalah alat yang digunakan untuk menginisialisasi dan mengelola cluster Kubernetes. Fungsi utamanya adalah untuk:

-Memudahkan proses instalasi dan konfigurasi Kubernetes di server.

-Membuat control plane dan worker node dengan cepat.

-Memungkinkan upgrade cluster dan melakukan tindakan pemeliharaan lainnya.

**Arsitektur:**

-Bootstrap: kubeadm digunakan untuk bootstrap cluster Kubernetes.

-Control Plane Initialization: Menginisialisasi komponen control plane seperti API server, scheduler, dan controller manager.

-Joining Nodes: Digunakan untuk menambahkan worker node ke cluster yang sudah ada dengan command kubeadm join.

Dengan kubeadm, administrator dapat dengan mudah mengelola lifecycle dari sebuah cluster Kubernetes, mulai dari inisialisasi hingga maintenance.
