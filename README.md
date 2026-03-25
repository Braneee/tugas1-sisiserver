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
git clone <URL_REPOSITORY>
cd <NAMA_FOLDER>

2. Jalankan Docker Compose
docker-compose up -d

3. Cek container berjalan
docker ps

4. Akses WordPress
http://localhost:8000

5. Lakukan instalasi WordPress
- Pilih bahasa
- Isi nama website
- Buat username admin
- Buat password admin
- Login ke dashboard
```
