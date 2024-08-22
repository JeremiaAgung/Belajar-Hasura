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

**Berikut adalah penjelasan dari beberapa perintah dan istilah terkait Docker:**

`docker ps`
Menampilkan daftar kontainer yang sedang berjalan. Jika ditambahkan flag -a, maka akan menampilkan semua kontainer, baik yang sedang berjalan maupun yang sudah berhenti.

`docker images`
Menampilkan daftar image Docker yang tersimpan di lokal. Ini mencakup nama image, tag, dan ukuran image.

`docker pull <image_name>`
Mengunduh image dari Docker Hub atau registry lainnya ke lokal. Misalnya, `docker pull ubuntu` akan mengunduh image Ubuntu.

`docker run <image_name>`
Menjalankan sebuah kontainer baru berdasarkan image yang ditentukan. Misalnya, `docker run ubuntu` akan menjalankan kontainer Ubuntu.

`docker exec -it <container_id> <command>`
Menjalankan perintah di dalam kontainer yang sedang berjalan. Misalnya, `docker exec -it <container_id>` bash akan membuka shell bash di dalam kontainer.

`docker stop <container_id>`
Menghentikan kontainer yang sedang berjalan.

`docker rm <container_id>`
Menghapus kontainer yang sudah berhenti. Untuk menghapus kontainer yang sedang berjalan, gunakan -f (force): `docker rm -f <container_id>`

`docker rmi <image_name>`
Menghapus image dari lokal. Jika image digunakan oleh satu atau lebih kontainer, image tersebut tidak bisa dihapus kecuali menggunakan flag -f.

`docker build -t <image_name>`
Membangun image Docker dari Dockerfile yang ada di direktori saat ini (.). Flag -t digunakan untuk memberi nama pada image yang dibangun.

`docker-compose up`
Menjalankan semua layanan yang didefinisikan dalam file docker-compose.yml. Jika ditambahkan flag -d, layanan akan berjalan di latar belakang (detached mode).

`docker-compose down`
Menghentikan dan menghapus semua kontainer, jaringan, dan volume yang dibuat oleh docker-compose up.

`docker logs <container_id>`
Menampilkan log dari kontainer yang sedang berjalan atau sudah berhenti.

`docker network ls`
Menampilkan daftar jaringan (network) yang ada di Docker.
**Penjelasan Mengenai Docker Network**

Docker Network adalah fitur yang memungkinkan kontainer dalam Docker untuk saling berkomunikasi. 

Ada beberapa jenis jaringan yang bisa digunakan:

**Bridge**: Jaringan default yang digunakan untuk menghubungkan kontainer di satu host.

**Host**: Kontainer menggunakan jaringan host langsung, tanpa isolasi.

**Overlay**: Menghubungkan kontainer di berbagai host dalam Docker Swarm atau Kubernetes.

**Macvlan**: Memberi kontainer MAC address sendiri untuk komunikasi langsung di jaringan fisik.

**None**: Kontainer tanpa koneksi jaringan.

Perintah dasar seperti docker network ls, create, connect, dan disconnect digunakan untuk mengelola jaringan ini.

![image](https://github.com/user-attachments/assets/4d45fcb1-623e-4778-b953-61bb010ad27c)

Berikut adalah gambar yang menggambarkan jenis-jenis Docker Network secara ringkas. Gambar ini menunjukkan bagaimana kontainer dalam jaringan Bridge, Host, Overlay, dan Macvlan berkomunikasi satu sama lain.


`docker volume ls` Menampilkan daftar volume yang ada di Docker.

konsep stateful dan stateless seringkali berkaitan dengan bagaimana aplikasi mengelola data dan bagaimana data tersebut dipertahankan atau tidak ketika kontainer dihentikan atau dihapus.

**1. Stateful Containers**

Stateful containers adalah kontainer yang mempertahankan data mereka bahkan setelah dihentikan atau dihapus. Untuk mencapai ini, Docker menggunakan volumes atau bind mounts yang memungkinkan data disimpan di luar siklus hidup kontainer. Data yang disimpan di volume Docker akan tetap ada bahkan jika kontainer yang menggunakannya dihentikan atau dihapus.

**Ciri-ciri Stateful Containers:**

Volume: Data disimpan di luar kontainer, biasanya di volume Docker. Data tetap ada setelah kontainer dihentikan atau dihapus.

Persistence: Digunakan untuk aplikasi yang memerlukan penyimpanan data jangka panjang, seperti basis data, file log, atau file konfigurasi.
Contoh: Database seperti MariaDB atau PostgreSQL yang menyimpan data di volume.

**2. Stateless Containers**

Stateless containers tidak menyimpan data apa pun yang tidak spesifik pada siklus hidup kontainer itu sendiri. Artinya, ketika kontainer dihentikan atau dihapus, semua data di dalamnya juga hilang. Data hanya ada selama kontainer aktif.

**Ciri-ciri Stateless Containers:**

No Volume: Tidak menggunakan volume atau bind mounts untuk penyimpanan data persisten.

Ephemeral Data: Data hanya ada selama kontainer hidup, dan akan hilang ketika kontainer dihentikan.

Contoh: Aplikasi web yang hanya memproses data sementara, seperti server HTTP yang hanya merespons permintaan dan tidak menyimpan data.

**Stateful Container:**

Sebuah gambar yang menunjukkan kontainer Docker dengan volume yang terhubung, di mana volume tersebut menyimpan data yang bertahan setelah kontainer dihentikan.

Stateless Container:

Sebuah gambar yang menunjukkan kontainer Docker tanpa volume, di mana semua data hilang ketika kontainer dihentikan.

![image](https://github.com/user-attachments/assets/28523b00-6abf-43df-976d-baa2f46eb87b)

Berikut adalah gambar yang menunjukkan perbedaan antara stateful dan stateless Docker containers. Pada sisi kiri, terlihat stateful container dengan volume yang terhubung, sementara di sisi kanan, terlihat stateless container tanpa volume yang terhubung. Ini menggambarkan bahwa data pada stateful container dipertahankan meskipun kontainer dihentikan, sedangkan pada stateless container data tidak bertahan setelah kontainer dihentikan.

`docker inspect <container_id>`
Menampilkan informasi detail tentang sebuah kontainer, termasuk konfigurasi, mount point, dan lain-lain.

```
Usage:  docker [OPTIONS] COMMAND [ARG...]

A self-sufficient runtime for containers.

Options:
  -D, --debug              Enable debug mode
  --help                    Print usage
  -H, --host string         Daemon socket(s) to connect to
  -l, --log-level string    Set the logging level
  --tls                     Use TLS; implied by --tlsverify
  --tlsverify               Use TLS and verify the remote
  --version                 Print version information and quit

Commands:
  attach                   Attach to a running container
  build                    Build an image from a Dockerfile
  compose                  Docker Compose (see `docker compose --help`)
  cp                       Copy files/folders between a container and the local filesystem
  create                   Create a new container
  diff                     Display changes to files and directories on a container’s filesystem
  events                   Get real time events from the server
  exec                     Run a command in a running container
  export                   Export a container’s filesystem as a tar archive
  history                  Show the history of an image
  images                   List images
  import                   Import the contents of a tarball to create a filesystem image
  info                     Display system-wide information
  inspect                  Return low-level information on Docker objects
  kill                     Kill one or more running containers
  load                     Load an image from a tar archive or STDIN
  logs                     Fetch the logs of a container
  network                  Manage Docker networks
  node                     Manage Docker nodes (Swarm mode)
  pause                    Pause one or more running containers
  plugin                   Manage Docker plugins
  port                     List port mappings or a specific mapping for the container
  ps                       List containers
  pull                     Pull an image or a repository from a registry
  push                     Push an image or a repository to a registry
  rename                   Rename a container
  restart                  Restart one or more containers
  rm                       Remove one or more containers
  rmi                      Remove one or more images
  run                      Run a command in a new container
  save                     Save an image to a tar archive
  search                   Search for an image in a registry
  start                    Start one or more stopped containers
  stats                    Display a live stream of container(s) resource usage statistics
  stop                     Stop one or more running containers
  tag                      Tag an image into a repository
  top                      Display the running processes of a container
  unpause                  Unpause one or more paused containers
  update                   Update configurations of one or more containers
  version                  Show the Docker version information
  volume                   Manage Docker volumes
  wait                     Block until one or more containers stop, then print their exit codes

```





