# DOCKER
Docker adalah platform untuk menjalankan aplikasi dalam kontainer, yang mengisolasi aplikasi dan semua dependensinya agar bisa berjalan konsisten di berbagai lingkungan.

### Cara Kerja Docker
Cara Kerja Docker:
Kontainerisasi: Mengisolasi aplikasi dalam kontainer.
Docker Image: Template yang digunakan untuk membuat kontainer.
Docker Engine: Runtime yang menjalankan kontainer.
Docker Hub: Tempat untuk menyimpan dan berbagi Docker image.
Perintah Docker:

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






