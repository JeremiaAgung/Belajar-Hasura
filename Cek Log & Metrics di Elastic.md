# Elasticsearch
adalah search engine dan sistem analitik terdistribusi berbasis open-source yang cepat, digunakan untuk pencarian teks, analisis data log, dan monitoring real-time. Dibangun di atas Apache Lucene, Elasticsearch sering digunakan bersama Kibana, Logstash, dan Beats dalam Elastic Stack untuk manajemen data skala besar.

Saya Menggunakan Elastic untuk mengecek logs dan Metrics

Menggunakan HIT pada Hasura di Postman `http://10.100.14.5:8084/v1/graphql`

**Status Success di Elastic Metrics**
```
{
  "_index": ".ds-metrics-generic-default-2024.12.06-000001",
  "_id": "iRI-m5MBatu-e5CD-5g9",
  "_version": 1,
  "_source": {
    "@timestamp": "2024-12-06T09:08:49.559434453Z",
    "data_stream": {
      "dataset": "generic",
      "namespace": "default",
      "type": "metrics"
    },
    "hasura_cron_events_invocation_total": 0,
    "hasura_cron_events_processed_total": 0,
    "hasura_oneoff_events_invocation_total": 0,
    "hasura_oneoff_events_processed_total": 0,
    "host": {
      "hostname": "hasura-jeremi-6896c47b9b-p2s7g:8080",
      "name": "hasura-jeremi-6896c47b9b-p2s7g:8080"
    },
    "service": {
      "name": "hasura"
    },
    "status": "success"
  },
  "fields": {
    "hasura_cron_events_processed_total": [
      0
    ],
    "@timestamp": [
      "2024-12-06T09:08:49.559Z"
    ],
    "service.name": [
      "hasura"
    ],
    "data_stream.namespace": [
      "default"
    ],
    "data_stream.dataset": [
      "generic"
    ],
    "hasura_cron_events_invocation_total": [
      0
    ],
    "hasura_oneoff_events_processed_total": [
      0
    ],
    "host.hostname": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "host.name": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "data_stream.type": [
      "metrics"
    ],
    "hasura_oneoff_events_invocation_total": [
      0
    ],
    "status": [
      "success"
    ]
  }
}
```
Penjelasan:
Metrik menunjukkan bahwa layanan Hasura berjalan normal (success) di host hasura-jeremi-6896c47b9b-p2s7g:8080, tetapi belum ada event cron atau one-off yang dijalankan atau diproses (0).

**Status Failed di Elastic Metrics**
```
{
  "_index": ".ds-metrics-generic-default-2024.12.06-000001",
  "_id": "ShJGm5MBatu-e5CDw6d1",
  "_version": 1,
  "_source": {
    "@timestamp": "2024-12-06T09:17:19.638971904Z",
    "data_stream": {
      "dataset": "generic",
      "namespace": "default",
      "type": "metrics"
    },
    "hasura_cron_events_invocation_total": 0,
    "hasura_cron_events_processed_total": 0,
    "hasura_oneoff_events_invocation_total": 0,
    "hasura_oneoff_events_processed_total": 0,
    "host": {
      "hostname": "hasura-jeremi-6896c47b9b-p2s7g:8080",
      "name": "hasura-jeremi-6896c47b9b-p2s7g:8080"
    },
    "service": {
      "name": "hasura"
    },
    "status": "failed"
  },
  "fields": {
    "hasura_cron_events_processed_total": [
      0
    ],
    "@timestamp": [
      "2024-12-06T09:17:19.638Z"
    ],
    "service.name": [
      "hasura"
    ],
    "data_stream.namespace": [
      "default"
    ],
    "data_stream.dataset": [
      "generic"
    ],
    "hasura_cron_events_invocation_total": [
      0
    ],
    "hasura_oneoff_events_processed_total": [
      0
    ],
    "host.hostname": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "host.name": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "data_stream.type": [
      "metrics"
    ],
    "hasura_oneoff_events_invocation_total": [
      0
    ],
    "status": [
      "failed"
    ]
  }
}
```
Penjelasan Dari Metrics tersebut diketahui bahwa Log ini menunjukkan pada 6 Desember 2024, tidak ada event cron atau one-off yang diproses atau dipanggil oleh Hasura, dan status sistemnya adalah "failed" (gagal).

**Status Miss di Elastic Metrics**

```
{
  "_index": ".ds-metrics-generic-default-2024.12.06-000001",
  "_id": "bxJIm5MBatu-e5CDI6kD",
  "_version": 1,
  "_source": {
    "@timestamp": "2024-12-06T09:18:49.651501057Z",
    "data_stream": {
      "dataset": "generic",
      "namespace": "default",
      "type": "metrics"
    },
    "hasura_cache_request_count": 0,
    "host": {
      "hostname": "hasura-jeremi-6896c47b9b-p2s7g:8080",
      "name": "hasura-jeremi-6896c47b9b-p2s7g:8080"
    },
    "service": {
      "name": "hasura"
    },
    "status": "miss"
  },
  "fields": {
    "@timestamp": [
      "2024-12-06T09:18:49.651Z"
    ],
    "service.name": [
      "hasura"
    ],
    "data_stream.namespace": [
      "default"
    ],
    "data_stream.dataset": [
      "generic"
    ],
    "host.hostname": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "host.name": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "data_stream.type": [
      "metrics"
    ],
    "hasura_cache_request_count": [
      0
    ],
    "status": [
      "miss"
    ]
  }
}
```
Penjelasan :
Log ini mencatat bahwa pada waktu tertentu, layanan Hasura tidak menemukan data di cache (status "miss") dan tidak ada permintaan cache yang tercatat (nilai 0).

**Status Miss di Elastic Metrics**

```
{
  "_index": ".ds-metrics-generic-default-2024.12.06-000001",
  "_id": "XBJJm5MBatu-e5CDDatl",
  "_version": 1,
  "_source": {
    "@timestamp": "2024-12-06T09:19:49.660906289Z",
    "data_stream": {
      "dataset": "generic",
      "namespace": "default",
      "type": "metrics"
    },
    "hasura_cache_request_count": 0,
    "host": {
      "hostname": "hasura-jeremi-6896c47b9b-p2s7g:8080",
      "name": "hasura-jeremi-6896c47b9b-p2s7g:8080"
    },
    "service": {
      "name": "hasura"
    },
    "status": "hit"
  },
  "fields": {
    "@timestamp": [
      "2024-12-06T09:19:49.660Z"
    ],
    "service.name": [
      "hasura"
    ],
    "data_stream.namespace": [
      "default"
    ],
    "data_stream.dataset": [
      "generic"
    ],
    "host.hostname": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "host.name": [
      "hasura-jeremi-6896c47b9b-p2s7g:8080"
    ],
    "data_stream.type": [
      "metrics"
    ],
    "hasura_cache_request_count": [
      0
    ],
    "status": [
      "hit"
    ]
  }
}
```

Penjelasan: 
Secara keseluruhan, log ini mencatat metrik terkait cache dari Hasura, yang tidak mencatat permintaan cache (hasura_cache_request_count adalah 0), dan menunjukkan bahwa layanan Hasura berjalan dengan baik (status adalah hit).


