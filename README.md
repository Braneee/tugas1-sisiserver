# WordPress CMS with Docker Compose, MySQL, and Redis

## Deskripsi

Project ini merupakan implementasi WordPress CMS menggunakan Docker Compose dengan MySQL sebagai database dan Redis sebagai object cache.

## Learning Objectives

- Memahami multi-container setup dengan Docker Compose
- Menggunakan service dependencies (`depends_on`)
- Memahami Docker networking antar container
- Menggunakan volume untuk persistence data
- Menggunakan environment variables
- Mengintegrasikan Redis sebagai object cache

---

## Struktur Services

Project ini memiliki 3 service utama:

1. **WordPress**
2. **MySQL**
3. **Redis**

---

## Cara Menjalankan

### 1. Clone repository

```bash
git clone (https://github.com/Braneee/tugas1-sisiserver.git)
cd tugas1-sisiserver

```

### 2. Jalankan Docker Compose
```bash
docker-compose up -d
```
![79aa77ba-6be9-4a4a-9762-7d90beabac2c](https://github.com/user-attachments/assets/8ecd625f-9033-48cc-9640-74cab49e303d)

### 3. Cek container berjalan
```bash
docker ps
```
![d934e968-a383-4372-9408-45247d8d5c69](https://github.com/user-attachments/assets/44a836d5-8cda-4062-84c1-a5859bffa426)

### 4. Akses WordPress
```bash
http://localhost:8000

```
### 5. Lakukan instalasi WordPress
- Pilih bahasa
![1e2a599b-a3d4-45a2-a0b1-cd14c750515d](https://github.com/user-attachments/assets/b77061d4-51b5-4798-9a5d-3b6720c7c4b5)

- Isi nama website
- Buat username admin
- Buat password admin
![95b3930b-3d26-40d9-a1ed-4597ae9430ad](https://github.com/user-attachments/assets/720eb804-6302-40a4-a0a0-1b647cce38b8)

- Login ke dashboard
![71b998e5-1cc1-4abe-a4b5-43c783799cb8](https://github.com/user-attachments/assets/e332b027-0615-46bc-9960-14aef5c42ff0)



### 6. Redis CLI Ping Test
```bash
docker exec -it redis_cache redis-cli ping
```
![3ec9dac9-de3f-4b4a-8550-4b995588ff4d](https://github.com/user-attachments/assets/18c8bbe5-8c26-4850-97f6-57861d8296d5)

### 7. Setup Plugin Redis

![efbfabf4-6f89-4197-93cf-237d471711ae](https://github.com/user-attachments/assets/71cb5ae9-b0ed-4afd-83c4-63c8c7efae6e)

![9dde46fc-f916-4a11-87fd-2dea5ef14d44](https://github.com/user-attachments/assets/9e383594-bb6b-4276-8e1b-fd355a755a8d)

### Jawaban Pertanyaan

1. Kenapa perlu volume untuk MySQL?
Volume diperlukan agar data database MySQL tetap tersimpan meskipun container dihentikan, direstart, atau dihapus lalu dibuat ulang. Tanpa volume, seluruh data seperti user, post, page, dan konfigurasi WordPress di database akan hilang karena data di dalam container bersifat sementara.

2. Apa fungsi depends_on?
depends_on berfungsi untuk mengatur urutan saat container dijalankan. Dalam kasus ini, service wordpress dibuat bergantung pada mysql dan redis, sehingga Docker Compose akan menjalankan container MySQL dan Redis lebih dulu sebelum WordPress. Namun, depends_on hanya mengatur urutan start, bukan menjamin service tersebut sudah benar-benar siap menerima koneksi.

3. Bagaimana cara WordPress container connect ke MySQL?
WordPress terhubung ke MySQL melalui Docker network internal. Karena kedua container berada pada network yang sama, WordPress bisa mengakses MySQL menggunakan nama service sebagai hostname, yaitu mysql. Itulah sebabnya WORDPRESS_DB_HOST diisi dengan mysql:3306. Jadi WordPress tidak memakai localhost, melainkan nama service container database.

4. Apa keuntungan pakai Redis untuk WordPress?
Redis digunakan sebagai object cache untuk menyimpan data sementara di memory, sehingga WordPress tidak perlu selalu mengambil data yang sama berulang-ulang dari MySQL. Keuntungannya adalah performa website menjadi lebih cepat, beban database berkurang, dan waktu respon aplikasi menjadi lebih baik, terutama saat website mulai sering diakses.


