# Hasura V2 - Troubleshooting Errors

## 1. Metadata Inconsistencies (Ketidaksesuaian Metadata)
### Penyebab:
- Perubahan skema database tanpa memperbarui metadata Hasura.
- Edit manual file metadata (tables.yaml, relationships.yaml).
- Konflik antara schema Hasura dan remote schema.
- Migrasi gagal atau tidak selesai.

### Gejala:
- Query atau mutation error: `field/table not found`.
- Schema tidak ditemukan atau metadata tidak konsisten.
- Perubahan skema database tidak tercermin di Hasura.

### Solusi:
#### **Reload Metadata** (jika perubahan kecil):
```sh
hasura metadata reload
```
#### **Reset Metadata** (jika metadata rusak total):
```sh
hasura metadata reset
```
#### **Verifikasi Remote Schema:**
- Pastikan remote schema valid dan diperbarui.

---

## 2. Timeout Database
### Penyebab:
- Query lama dieksekusi (karena data besar atau indeks kurang optimal).
- Koneksi terputus atau server kekurangan sumber daya.
- `statement_timeout` di PostgreSQL terlalu ketat.

### Gejala:
- Error: `"canceling statement due to statement timeout"`.
- Query tidak selesai atau sering terputus.
- Performa aplikasi lambat atau gagal merespons.

### Solusi:
#### **Atur Timeout di Database:**
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: postgres-config
  namespace: your-namespace
data:
  postgresql.conf: |
    statement_timeout = 5000
```

#### **Atur Timeout di Hasura:**
```yaml
env:
  - name: HASURA_GRAPHQL_SERVER_TIMEOUT
    value: "30000"
  - name: HASURA_GRAPHQL_EXECUTE_TIMEOUT
    value: "30000"
```

#### **Optimalkan Query:**
- Tambahkan indeks yang tepat.
- Sederhanakan penggunaan `JOIN` jika memungkinkan.
- Gunakan `EXPLAIN ANALYZE` untuk melihat performa query.

#### **Pantau Log & Monitoring:**
- Aktifkan logging untuk melihat query lambat.
- Gunakan tools seperti Prometheus dan Grafana.

---

## 3. TPS Error (Transaction Per Second Error)
### Penyebab:
- Query sering gagal karena timeout atau koneksi buruk.
- Beban sistem tinggi menyebabkan transaksi gagal.

### Gejala:
- Transaksi sering gagal.
- Error query/mutation meningkat di log Hasura.
- Kinerja aplikasi turun.

### Solusi:
#### **Monitor TPS Error:**
- Gunakan Grafana, Prometheus, atau Datadog untuk melihat metrik TPS.

#### **Optimalkan Query:**
- Identifikasi query yang sering gagal dan perbaiki.
- Pastikan query tidak terlalu berat.

#### **Atur Timeout yang Wajar:**
- Sesuaikan `statement_timeout` dengan ekspektasi eksekusi query.

#### **Pastikan Sumber Daya Cukup:**
- Cek penggunaan CPU dan memori pada Hasura & database.

---

## 4. Authentication & Authorization Errors
### Penyebab:
- JWT tidak valid atau expired.
- Role tidak memiliki izin yang cukup.
- Konfigurasi `HASURA_GRAPHQL_JWT_SECRET` salah.

### Gejala:
- Error: `"JWT token is invalid"` atau `"unauthorized"`.
- Query/mutation ditolak meskipun login berhasil.

### Solusi:
#### **Periksa JWT Token:**
- Pastikan format, validitas, dan expiry token.

#### **Perbaiki Konfigurasi JWT:**
```json
{
  "type": "RS256",
  "key": "<public-key>"
}
```

#### **Cek Role & Permissions:**
- Pastikan role memiliki izin yang sesuai.
- Sesuaikan row-level security dan field-level permissions.

#### **Periksa Header Otorisasi:**
- Pastikan client mengirimkan header dengan benar.

---

Dengan memahami dan menerapkan solusi ini, error pada Hasura V2 dapat diatasi secara efektif. 🚀
