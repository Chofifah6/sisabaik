# SisaBaik

SisaBaik adalah proyek berkembang pada mata kuliah Pengembangan Web. Aplikasi ini dirancang untuk membantu penyedia memulihkan nilai stok makanan berlebih melalui penjualan dengan harga khusus atau penyaluran, sekaligus membantu masyarakat memperoleh makanan yang lebih terjangkau dan mengurangi limbah pangan.

## Capaian Chapter 8

- Menambahkan migrasi skema basis data `database/07_auth.sql` untuk mendukung entitas pengguna, sesi autentikasi, dan peran (*role-based access control*).
- Menyediakan fitur pendaftaran mandiri untuk dua peran utama: **pembeli** (`/api/auth/registrasi`) dan **penyedia** (`/api/auth/registrasi-penyedia`).
- Mengimplementasikan alur peninjauan dan verifikasi penyedia oleh pengelola melalui skrip CLI (`npm run penyedia:verifikasi`).
- Menerapkan pengamanan JWT (JSON Web Token) dengan validasi regex yang mendukung karakter base64url dan pemutus sesi (*logout* seluruh sesi melalui peningkatan versi token).
- Menambahkan antarmuka pengujian visual mandiri (`public/auth.html`) serta pengujian otomatis berbasis skrip (`npm run auth:test`).

## Prasyarat & Lingkungan

- Node.js: v18.x atau lebih baru
- PostgreSQL: v14.x atau lebih baru
- Basis data `sisabaik_dev` sudah dikonfigurasi dan menjalankan migrasi dari `01_schema.sql` hingga `07_auth.sql`.
- Berkas `.env` telah dikonfigurasi tanpa menyertakan nilai rahasia di repositori.

### Variabel Lingkungan (`.env`)
```env
PGHOST=localhost
PGPORT=5432
PGDATABASE=sisabaik_dev
PGUSER=postgres
PGPASSWORD=password_anda
JWT_SECRET=kunci_rahasia_praktikum_anda