# SisaBaik

SisaBaik adalah proyek berkembang pada mata kuliah Pengembangan Web. Aplikasi ini dirancang untuk membantu penyedia memulihkan nilai stok makanan berlebih melalui penjualan dengan harga khusus atau penyaluran, sekaligus membantu masyarakat memperoleh makanan yang lebih terjangkau dan mengurangi limbah pangan.

## Capaian Modul / Chapter

### Capaian Chapter 9 (Membangun Antarmuka dengan Vue)
- Membangun antarmuka frontend berbasis komponen Vue 3 (Composition API & Single-File Components).
- Mengintegrasikan manajemen state reaktif (`ref`) dan data turunan (`computed`) untuk kalkulasi ketersediaan, filter katalog, serta validasi form.
- Menyusun alur komunikasi data antar-komponen menggunakan *props* dan *emits*.
- Menyiapkan aset visual SVG lokal (`brand-mark.svg`, `food-bread.svg`, `food-bowl.svg`, `food-produce.svg`) dan komponen `Ikon.vue`.
- Menggunakan 6 data *fixture* di memori browser untuk simulasi antarmuka pembeli dan penyedia tanpa memanggil REST API backend.
- Menyiapkan server pengembangan dan proses kompilasi produksi menggunakan Vite (`dev`, `build`, `preview`).

### Capaian Chapter 8 (Autentikasi & Otorisasi Backend)
- Menambahkan migrasi skema basis data `database/07_auth.sql` untuk mendukung entitas pengguna, sesi autentikasi, dan peran (*role-based access control*).
- Menyediakan fitur pendaftaran mandiri untuk dua peran utama: **pembeli** (`/api/auth/registrasi`) dan **penyedia** (`/api/auth/registrasi-penyedia`).
- Mengimplementasikan alur peninjauan dan verifikasi penyedia oleh pengelola melalui skrip CLI (`npm run penyedia:verifikasi`).
- Menerapkan pengamanan JWT (JSON Web Token) dengan validasi regex yang mendukung karakter base64url dan pemutus sesi (*logout* seluruh sesi melalui peningkatan versi token).
- Menambahkan antarmuka pengujian visual mandiri (`public/auth.html`) serta pengujian otomatis berbasis skrip (`npm run auth:test`).

## Prasyarat & Lingkungan

- **Node.js**: `^22.18.0` atau `>=24.12.0`
- **npm**: Versi bawaan Node.js
- **PostgreSQL**: v14.x atau lebih baru (untuk backend Modul 8)
- **Editor**: Visual Studio Code dengan ekstensi **Vue - Official**

### Variabel Lingkungan Backend (`.env`)
```env
PGHOST=localhost
PGPORT=5432
PGDATABASE=sisabaik_dev
PGUSER=postgres
PGPASSWORD=password_anda
JWT_SECRET=kunci_rahasia_praktikum_anda
```

---

## Petunjuk Menjalankan Aplikasi

### 1. Backend Express (Modul 8)
Backend tetap berada di root repositori untuk kebutuhan autentikasi dan integrasi mendatang pada Pertemuan 11.
```bash
npm install
npm run dev
```

### 2. Frontend Vue 3 & Vite (Modul 9)
Seluruh kode antarmuka frontend dikelola di dalam subfolder `frontend/`.

```bash
# Pindah ke folder frontend
cd frontend

# Instalasi dependency frontend
npm install
# atau menggunakan npm ci jika memakai package-lock.json

# Jalankan server pengembang (Development Server)
npm run dev
# Akses aplikasi di: http://127.0.0.1:5173/

# Kompilasi produksi (Build)
npm run build

# Menjalankan preview hasil build secara lokal
npm run preview
# Akses preview di: http://127.0.0.1:4173/
```

---

## Catatan Arsitektur & Fixture Memori (Chapter 9)

- **Simulasi Browser (Tanpa Request API)**: Pada Modul 9, antarmuka berjalan menggunakan 6 data *fixture* lokal di memori browser (`src/data/penawaran-latihan.js`). Browser belum melakukan panggilan API HTTP ke backend Express.
- **Backend Tetap Mempertahankan Fitur Modul 8**: Pendaftaran mandiri, verifikasi penyedia, autentikasi JWT, dan otorisasi RBAC backend Modul 8 tetap dipertahankan pada root proyek untuk diintegrasikan pada Pertemuan 11.
- **Aset Visual SVG Lokal**: Seluruh ilustrasi dan logo menggunakan berkas SVG lokal (`brand-mark.svg`, `food-bread.svg`, `food-bowl.svg`, `food-produce.svg`) yang dikelola otomatis oleh Vite tanpa dependensi CDN luar.