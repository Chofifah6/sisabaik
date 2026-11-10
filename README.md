# SisaBaik

SisaBaik adalah proyek full-stack pengembangan web yang dikembangkan untuk mata kuliah Pengembangan Web. Aplikasi ini menghubungkan penyedia makanan berlebih dengan pembeli melalui katalog interaktif, autentikasi berbasis peran, dan alur transaksi terintegrasi.

## Developed By Chofifah Humayra

---

## Capaian Modul 10 (Integrasi Full Stack Vue & REST API)

- **Integrasi End-to-End**: Menghubungkan antarmuka komponen Vue 3 dengan backend REST API Express dan basis data PostgreSQL[cite: 1, 2].
- **Autentikasi & Sesi**: Menerapkan pendaftaran mandiri (pembeli & penyedia), manajemen sesi berbasis JWT di memori, serta perlindungan route via *navigation guards*[cite: 3, 5, 7, 34, 40, 68].
- **Manajemen Penawaran & Foto**: Fitur CRUD penawaran milik penyedia dengan unggah foto opsional (konversi WebP via `sharp`) dan pencegahan konflik edisi (*optimistic concurrency control* via versi DTO)[cite: 2, 4, 6, 17, 24, 48, 49].
- **Alur Transaksi & Stok**: Pemesanan makanan, reservasi & pemulihan stok otomatis, pembatalan/penolakan dengan alasan, serta pencatatan serah terima (berbayar/gratis di tempat)[cite: 1, 2, 8, 9, 10, 58, 59].
- **Dashboard Agregat**: Menampilkan metrik analitik bisnis secara *real-time* sesuai peran akun (total belanja, pendapatan, penghematan, dan unit tersalurkan)[cite: 1, 3, 9, 10, 62, 63, 64].
- **Build & Single Origin**: Mengompilasi aplikasi frontend menggunakan Vite dan menyajikannya bersama backend Express dalam satu port (*single origin* di port 3000)[cite: 4, 11, 16, 78].

---

## Prasyarat & Lingkungan

- **Node.js**: `^22.18.0` atau `>=24.12.0`[cite: 11, 19]
- **PostgreSQL**: v14.x atau lebih baru[cite: 11]
- **Editor**: Visual Studio Code (dengan ekstensi Vue - Official)[cite: 11]

### Variabel Lingkungan Backend (`.env`)
```env
PGHOST=127.0.0.1
PGPORT=5432
PGDATABASE=sisabaik_dev
PGUSER=postgres
PGPASSWORD=password_anda
JWT_SECRET=kunci_rahasia_praktikum_anda
NODE_ENV=development
HOST=127.0.0.1
TRUST_PROXY_HOPS=0
PGSSL=disable