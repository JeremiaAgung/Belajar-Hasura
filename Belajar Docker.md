### DOCKER
Docker adalah platform yang memungkinkan pengembang untuk mengotomatisasi penyebaran aplikasi dalam bentuk kontainer. Kontainer adalah unit perangkat lunak yang mengemas kode aplikasi dan semua dependensi yang diperlukan untuk menjalankannya sehingga aplikasi tersebut dapat berjalan secara konsisten di berbagai lingkungan, baik itu di mesin pengembangan lokal, server staging, atau produksi.

### Cara Kerja Docker
Kontainerisasi: Docker memanfaatkan teknologi kontainerisasi untuk mengisolasi aplikasi dan dependensinya dalam satu paket mandiri yang disebut kontainer. Kontainer ini bisa berjalan di mana saja tanpa perlu menyesuaikan sistem operasi atau lingkungan.

Docker Engine: Ini adalah runtime yang mengelola kontainer Docker. Docker Engine memungkinkan Anda untuk membangun, menjalankan, dan mengelola kontainer.

Dockerfile: Ini adalah file teks yang berisi instruksi untuk membangun image Docker. Setiap instruksi dalam Dockerfile akan dieksekusi secara berurutan untuk membuat image Docker yang bisa digunakan untuk menjalankan kontainer.

Docker Image: Ini adalah snapshot dari sebuah aplikasi dan semua dependensinya, yang dibuat dari Dockerfile. Docker Image ini bersifat read-only, dan dari sinilah kontainer Docker dijalankan.

Docker Hub: Ini adalah registry publik tempat Anda dapat menyimpan, berbagi, dan mengelola image Docker. Anda bisa menarik (pull) image dari Docker Hub atau mendorong (push) image Anda sendiri ke Docker Hub.

Docker Compose: Ini adalah alat yang memungkinkan Anda untuk mendefinisikan dan menjalankan aplikasi multi-kontainer. Anda dapat menggunakan file docker-compose.yml untuk mengkonfigurasi layanan, jaringan, dan volume yang dibutuhkan oleh aplikasi.

Docker Swarm: Ini adalah alat orkestrasi yang memungkinkan pengelolaan cluster kontainer Docker secara otomatis. Dengan Docker Swarm, Anda bisa mengelola banyak kontainer yang berjalan di berbagai host sebagai satu kesatuan.
