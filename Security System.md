# Hasura GraphQL dan Keamanan (Firewall, DNS, Network Policy)

Hasura GraphQL dapat berinteraksi dengan sistem keamanan seperti **Firewall, DNS, dan Network Policy** untuk memastikan komunikasi yang aman antara klien dan server GraphQL.

## 1. Firewall dan Hasura GraphQL

### 🔹 Peran Firewall dalam Keamanan Hasura
Firewall melindungi Hasura dari akses yang tidak sah melalui berbagai cara:
- **Firewall Jaringan**: Membatasi IP yang dapat mengakses Hasura.
- **Firewall Aplikasi (WAF)**: Melindungi dari serangan seperti **SQL Injection, XSS, dan DDoS**.
- **Firewall Kubernetes (Network Policy)**: Membatasi komunikasi antar pod di Kubernetes.

### 🔹 Konfigurasi Firewall untuk Hasura
- **Buka port yang dibutuhkan** (misalnya, **port 8080** untuk Hasura di Docker/Kubernetes).
- **Batasi akses hanya dari IP tertentu**.
- **Gunakan WAF** untuk mendeteksi permintaan berbahaya.

#### Contoh: Menggunakan IPTables untuk membatasi akses ke Hasura
```sh
iptables -A INPUT -p tcp --dport 8080 -s 192.168.1.100 -j ACCEPT
iptables -A INPUT -p tcp --dport 8080 -j DROP
```
- **Hanya IP 192.168.1.100 yang bisa mengakses Hasura** di port **8080**.
- **Semua akses lain akan diblokir**.

---

## 2. DNS dan Hasura GraphQL

### 🔹 Peran DNS dalam Keamanan Hasura
- **DNS digunakan untuk menentukan domain Hasura** (misalnya, `hasura.example.com`).
- **Gunakan DNS-over-HTTPS (DoH) atau DNS-over-TLS (DoT)** untuk mencegah **DNS Spoofing**.
- **Gunakan Load Balancer berbasis DNS** (misalnya, **Cloudflare, AWS Route 53**).

### 🔹 Konfigurasi DNS untuk Hasura
- Tambahkan **A Record** untuk `hasura.example.com` yang mengarah ke IP server Hasura.
- Gunakan **Proxy Mode** di Cloudflare untuk menyembunyikan IP asli.
- Aktifkan **Rate Limiting** untuk melindungi dari DDoS.

Jika Hasura berjalan dalam **Kubernetes**, gunakan **CoreDNS** untuk resolusi DNS internal antar layanan.

---

## 3. Network Policy dan Hasura GraphQL

### 🔹 Peran Network Policy dalam Hasura
Jika Hasura berjalan di **Kubernetes**, gunakan **NetworkPolicy** untuk:
- **Hanya izinkan akses dari layanan backend tertentu** ke Hasura.
- **Blokir akses dari layanan yang tidak diizinkan**.

### 🔹 Contoh Network Policy untuk Hasura di Kubernetes
```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-backend-to-hasura
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
- **Hanya pod dengan label `app=backend` yang bisa mengakses Hasura di port 8080**.
- **Layanan lain tidak akan bisa mengakses Hasura**.

---

## Kesimpulan
Hasura GraphQL dapat diamankan dengan:
✅ **Firewall** → Mencegah akses tidak sah dan serangan jaringan.
✅ **DNS** → Mencegah DNS Spoofing dan serangan berbasis resolusi nama.
✅ **Network Policy** → Mengontrol akses dalam Kubernetes.

