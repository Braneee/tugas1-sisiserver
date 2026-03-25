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
<img width="905" height="315" alt="image" src="https://github.com/user-attachments/assets/3ad461b6-6093-4008-9627-dc93c93f692a" />

```

### 3. Cek container berjalan
```bash
docker ps
<img width="1419" height="114" alt="image" src="https://github.com/user-attachments/assets/ac03c82e-aa74-404f-9f14-23cf771ac437" />

```
### 4. Akses WordPress
```bash
http://localhost:8000

```
### 5. Lakukan instalasi WordPress
```bash
- Pilih bahasa
<img width="1600" height="817" alt="image" src="https://github.com/user-attachments/assets/ebb395a6-5cd6-4429-bdac-2f248ad069de" />
- Isi nama website
- Buat username admin
- Buat password admin
<img width="1600" height="812" alt="image" src="https://github.com/user-attachments/assets/dec8889f-8387-4398-a38e-4643bdcc4368" />
- Login ke dashboard
<img width="1600" height="818" alt="image" src="https://github.com/user-attachments/assets/19570900-3879-4f89-a085-08c5c5be3462" />

```

### 6. Redis CLI Ping Test
```bash
docker exec -it redis_cache redis-cli ping
<img width="674" height="43" alt="image" src="https://github.com/user-attachments/assets/33f37f1a-0058-4ef3-b3e4-3780de8f9721" />

```

### 7. Setup Plugin Redis
```bash
<img width="1600" height="851" alt="image" src="https://github.com/user-attachments/assets/b785206d-9593-43eb-9aac-e1a35adabadf" />
=<img width="1600" height="855" alt="image" src="https://github.com/user-attachments/assets/d8b69392-7a86-423d-a332-d73b60d65ea5" />

```

### Jawaban Pertanyaan
```bash
1. Kenapa perlu volume untuk MySQL?
Volume diperlukan agar data database MySQL tetap tersimpan meskipun container dihentikan, direstart, atau dihapus lalu dibuat ulang. Tanpa volume, seluruh data seperti user, post, page, dan konfigurasi WordPress di database akan hilang karena data di dalam container bersifat sementara.

2. Apa fungsi depends_on?
depends_on berfungsi untuk mengatur urutan saat container dijalankan. Dalam kasus ini, service wordpress dibuat bergantung pada mysql dan redis, sehingga Docker Compose akan menjalankan container MySQL dan Redis lebih dulu sebelum WordPress. Namun, depends_on hanya mengatur urutan start, bukan menjamin service tersebut sudah benar-benar siap menerima koneksi.

3. Bagaimana cara WordPress container connect ke MySQL?
WordPress terhubung ke MySQL melalui Docker network internal. Karena kedua container berada pada network yang sama, WordPress bisa mengakses MySQL menggunakan nama service sebagai hostname, yaitu mysql. Itulah sebabnya WORDPRESS_DB_HOST diisi dengan mysql:3306. Jadi WordPress tidak memakai localhost, melainkan nama service container database.

4. Apa keuntungan pakai Redis untuk WordPress?
Redis digunakan sebagai object cache untuk menyimpan data sementara di memory, sehingga WordPress tidak perlu selalu mengambil data yang sama berulang-ulang dari MySQL. Keuntungannya adalah performa website menjadi lebih cepat, beban database berkurang, dan waktu respon aplikasi menjadi lebih baik, terutama saat website mulai sering diakses.
```

