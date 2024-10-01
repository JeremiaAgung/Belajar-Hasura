HTTP Requests & Responses:
hasura_action_request_bytes_total dan hasura_action_response_bytes_total: Mengukur total ukuran badan request dan response HTTP melalui actions Hasura.
hasura_http_request_bytes_total dan hasura_http_response_bytes_total: Menghitung ukuran total request dan response HTTP di server HTTP.

Subscriptions:
hasura_active_subscription_pollers: Mengukur jumlah poller aktif untuk subscription (live query atau streaming).
hasura_active_subscription_pollers_in_error_state: Mengukur jumlah poller aktif yang berada dalam keadaan error.

Event Triggers:
hasura_event_trigger_http_workers: Mengukur jumlah pekerja HTTP yang aktif untuk event trigger.
hasura_event_trigger_request_bytes_total dan hasura_event_trigger_response_bytes_total: Mengukur ukuran total request dan response melalui event trigger.

GraphQL:
hasura_graphql_requests_total: Menghitung total request GraphQL (query atau mutation).
hasura_graphql_execution_time_seconds: Mengukur waktu eksekusi request GraphQL yang sukses.

WebSockets:
hasura_websocket_connections: Mengukur jumlah koneksi WebSocket yang aktif.
hasura_websocket_message_queue_time dan hasura_websocket_message_write_time: Mengukur waktu pesan WebSocket berada di antrean dan waktu untuk menulis pesan ke buffer TCP.

Cron & One-off Events:
hasura_cron_events_invocation_total dan hasura_oneoff_events_invocation_total: Mengukur jumlah event cron dan one-off yang dijalankan dan apakah berhasil atau gagal.
Secara keseluruhan, metrik-metrik ini memberikan informasi tentang kinerja dan aktivitas berbagai komponen dari Hasura, termasuk action, event triggers, GraphQL, WebSocket, dan scheduled events.
