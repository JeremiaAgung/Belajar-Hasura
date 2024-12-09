# Elasticsearch
adalah search engine dan sistem analitik terdistribusi berbasis open-source yang cepat, digunakan untuk pencarian teks, analisis data log, dan monitoring real-time. Dibangun di atas Apache Lucene, Elasticsearch sering digunakan bersama Kibana, Logstash, dan Beats dalam Elastic Stack untuk manajemen data skala besar.

Saya Menggunakan Elastic untuk mengecek logs dan Metrics

*Status Success*
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
