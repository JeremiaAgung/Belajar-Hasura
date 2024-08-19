# DOCKER
Docker adalah platform untuk menjalankan aplikasi dalam kontainer, yang mengisolasi aplikasi dan semua dependensinya agar bisa berjalan konsisten di berbagai lingkungan.

### Cara Kerja Docker

**Kontainerisasi:** Mengisolasi aplikasi dalam kontainer.

**Docker Image:** Template yang digunakan untuk membuat kontainer.

**Docker Engine:** Runtime yang menjalankan kontainer.

**Docker Hub:** Tempat untuk menyimpan dan berbagi Docker image.

### Perintah Docker:

docker run [image]: Menjalankan kontainer dari sebuah image.
Contoh: `docker run -d nginx`

docker ps: Menampilkan daftar kontainer yang sedang berjalan.

docker build -t [image-name]: Membangun image dari Dockerfile.
Contoh: `docker build -t myapp`

docker pull [image]: Mengambil image dari Docker Hub.
Contoh: `docker pull ubuntu`

docker push [image]: Mengirim image ke Docker Hub.
Contoh: `docker push myapp`

docker exec -it [container] [command]: Menjalankan perintah di dalam kontainer.
Contoh: `docker exec -it mycontainer bash`

`docker stop [container]`: Menghentikan kontainer yang sedang berjalan.

`docker rm [container]`: Menghapus kontainer yang sudah dihentikan.

`docker rmi [image]`: Menghapus image dari sistem lokal.

Berikut adalah penjelasan dari beberapa perintah dan istilah terkait Docker:

docker ps
Menampilkan daftar kontainer yang sedang berjalan. Jika ditambahkan flag -a, maka akan menampilkan semua kontainer, baik yang sedang berjalan maupun yang sudah berhenti.

docker images
Menampilkan daftar image Docker yang tersimpan di lokal. Ini mencakup nama image, tag, dan ukuran image.

docker pull <image_name>
Mengunduh image dari Docker Hub atau registry lainnya ke lokal. Misalnya, docker pull ubuntu akan mengunduh image Ubuntu.

docker run <image_name>
Menjalankan sebuah kontainer baru berdasarkan image yang ditentukan. Misalnya, docker run ubuntu akan menjalankan kontainer Ubuntu.

docker exec -it <container_id> <command>
Menjalankan perintah di dalam kontainer yang sedang berjalan. Misalnya, docker exec -it <container_id> bash akan membuka shell bash di dalam kontainer.

docker stop <container_id>
Menghentikan kontainer yang sedang berjalan.

docker rm <container_id>
Menghapus kontainer yang sudah berhenti. Untuk menghapus kontainer yang sedang berjalan, gunakan -f (force): docker rm -f <container_id>.

docker rmi <image_name>
Menghapus image dari lokal. Jika image digunakan oleh satu atau lebih kontainer, image tersebut tidak bisa dihapus kecuali menggunakan flag -f.

docker build -t <image_name> .
Membangun image Docker dari Dockerfile yang ada di direktori saat ini (.). Flag -t digunakan untuk memberi nama pada image yang dibangun.

docker-compose up
Menjalankan semua layanan yang didefinisikan dalam file docker-compose.yml. Jika ditambahkan flag -d, layanan akan berjalan di latar belakang (detached mode).

docker-compose down
Menghentikan dan menghapus semua kontainer, jaringan, dan volume yang dibuat oleh docker-compose up.

docker logs <container_id>
Menampilkan log dari kontainer yang sedang berjalan atau sudah berhenti.

docker network ls
Menampilkan daftar jaringan (network) yang ada di Docker.

docker volume ls
Menampilkan daftar volume yang ada di Docker.

docker inspect <container_id>
Menampilkan informasi detail tentang sebuah kontainer, termasuk konfigurasi, mount point, dan lain-lain.





