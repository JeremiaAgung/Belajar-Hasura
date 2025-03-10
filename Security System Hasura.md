# Hasura GraphQL dan Keamanan (Firewall, DNS, Network Policy)

Hasura GraphQL dapat berinteraksi dengan sistem keamanan seperti Firewall, DNS, dan Network Policy untuk memastikan komunikasi yang aman antara klien dan server GraphQL.

## 1. Firewall

Firewall memainkan peran penting dalam mengamankan Hasura GraphQL Engine dengan membatasi akses yang tidak sah, memblokir serangan berbahaya, dan mengontrol lalu lintas jaringan.

### Peran Firewall dalam Keamanan Hasura

#### 1. Firewall Jaringan (Network Firewall)

**Fungsi:** Membatasi akses ke Hasura berdasarkan alamat IP atau range IP tertentu.

**Manfaat:**
- Mencegah akses dari IP yang tidak dikenal atau tidak dipercaya.
- Membatasi akses hanya dari jaringan internal atau aplikasi klien yang sah.

**Contoh Konfigurasi AWS Security Group:**
```sh
aws ec2 authorize-security-group-ingress --group-id sg-12345678 --protocol tcp --port 8080 --cidr 192.168.1.0/24
```

#### 2. Firewall Aplikasi (Web Application Firewall - WAF)

**Fungsi:** Melindungi dari serangan seperti SQL Injection, XSS, dan DDoS.

**Contoh Konfigurasi NGINX dengan ModSecurity:**
```sh
sudo apt install libnginx-mod-security
sudo systemctl restart nginx
```

#### 3. Firewall Kubernetes (Network Policy)

**Fungsi:** Mengontrol komunikasi antar pod.

**Contoh Network Policy:**
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: hasura-network-policy
spec:
  podSelector:
    matchLabels:
      app: hasura
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: frontend
      ports:
        - protocol: TCP
          port: 8080
```

## 2. Konfigurasi Firewall

### 1. Membuka Port yang Dibutuhkan
```sh
sudo ufw allow 8080/tcp
```

### 2. Membatasi Akses Berdasarkan IP
```sh
iptables -A INPUT -p tcp --dport 8080 -s 192.168.1.100 -j ACCEPT
iptables -A INPUT -p tcp --dport 8080 -j DROP
```

### 3. Menggunakan WAF
```sh
aws waf create-web-acl --name "HasuraWAF" --metric-name "HasuraWAF" --default-action Type=ALLOW
```

### 4. Menyimpan Aturan IPTables
```sh
sudo iptables-save > /etc/iptables/rules.v4
```

### 5. Verifikasi Aturan
```sh
iptables -L -n -v
```

## 3. DNS (Domain Name System)

DNS memainkan peran penting dalam mengamankan dan mengelola akses ke Hasura GraphQL Engine. DNS tidak hanya digunakan untuk mengarahkan domain ke server Hasura, tetapi juga dapat digunakan untuk meningkatkan keamanan, kinerja, dan ketersediaan.

### Peran DNS dalam Keamanan Hasura

1. **Resolusi Nama Domain**
   - DNS digunakan untuk memetakan nama domain (misalnya, hasura.example.com) ke alamat IP server tempat Hasura di-host.
   - Ini memungkinkan pengguna atau aplikasi untuk mengakses Hasura menggunakan nama domain yang mudah diingat, bukan alamat IP.

2. **Mencegah DNS Spoofing**
   - Menggunakan DNS-over-HTTPS (DoH) dan DNS-over-TLS (DoT) untuk mengenkripsi permintaan DNS agar tidak mudah disadap atau dimanipulasi.

3. **Load Balancing berbasis DNS**
   - Round Robin DNS
   - Weighted Routing
   - Latency-based Routing

4. **Menyembunyikan IP Asli**
   - Menggunakan Proxy Mode di Cloudflare untuk melindungi server dari serangan langsung.

5. **Rate Limiting**
   - Cloudflare dapat membatasi jumlah permintaan yang masuk untuk menghindari serangan DDoS.

6. **Resolusi DNS Internal di Kubernetes**
   - Menggunakan CoreDNS untuk resolusi DNS antar layanan dalam Kubernetes.

### Konfigurasi DNS untuk Hasura

1. **Tambahkan A Record untuk Domain Hasura**
   - Nama: hasura.example.com
   - Tipe: A
   - Nilai: 203.0.113.10 (IP server Hasura)
   - TTL: Otomatis

2. **Gunakan Proxy Mode di Cloudflare**
   - Aktifkan ikon awan oranye untuk menyembunyikan IP asli server.

3. **Aktifkan DNS-over-HTTPS (DoH) atau DNS-over-TLS (DoT)**
   - Gunakan layanan Cloudflare (1.1.1.1) untuk keamanan tambahan.

4. **Aktifkan Rate Limiting di Cloudflare**
   - Batasi 100 permintaan per menit dari satu IP.

5. **Load Balancer (Opsional)**
   - Gunakan AWS Route 53 untuk mendistribusikan lalu lintas ke beberapa server.

6. **Konfigurasi CoreDNS untuk Kubernetes**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: coredns
  namespace: kube-system
data:
  Corefile: |
    .:53 {
        errors
        health
        ready
        kubernetes cluster.local in-addr.arpa ip6.arpa {
            pods insecure
            fallthrough in-addr.arpa ip6.arpa
        }
        prometheus :9153
        forward . /etc/resolv.conf
        cache 30
        loop
        reload
        loadbalance
    }
```

## 4. Network Policy untuk Hasura di Kubernetes

(Network Policy adalah fitur penting di Kubernetes yang memungkinkan mengontrol lalu lintas jaringan antara pod. Ketika Hasura GraphQL Engine di-deploy di Kubernetes, Network Policy dapat digunakan untuk membatasi akses ke Hasura hanya dari layanan atau pod tertentu, sehingga meningkatkan keamanan dan isolasi. Berikut adalah penjelasan detail tentang peran Network Policy dalam mengamankan Hasura dan contoh konfigurasinya:)

### Contoh Network Policy untuk Hasura di Kubernetes

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-backend-to-hasura
  namespace: default
spec:
  podSelector:
    matchLabels:
      app: hasura
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: backend
    ports:
    - protocol: TCP
      port: 8080
```

### Contoh Network Policy untuk Namespace Tertentu

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-backend-to-hasura
  namespace: hasura-namespace
spec:
  podSelector:
    matchLabels:
      app: hasura
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          project: backend
      podSelector:
        matchLabels:
          app: backend
    ports:
    - protocol: TCP
      port: 8080
```

## Kesimpulan
Dengan konfigurasi Firewall dan DNS yang tepat, Hasura dapat:
- Membatasi akses hanya dari sumber yang dipercaya.
- Melindungi dari serangan seperti SQL Injection, XSS, DDoS, dan DNS Spoofing.
- Mengontrol komunikasi antar pod di Kubernetes.
- Meningkatkan kinerja dan ketersediaan dengan Load Balancing berbasis DNS.

Menggunakan layanan seperti Cloudflare dan AWS Route 53 akan memberikan perlindungan tambahan serta memastikan Hasura tetap aman dan dapat diakses dengan andal.)
