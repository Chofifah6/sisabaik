# SisaBaik

SisaBaik adalah aplikasi web full-stack yang dikembangkan untuk mata kuliah Pengembangan Web (`DGT1.62.7009`), Program Studi S1 Bisnis Digital, Universitas Negeri Padang. Aplikasi ini menghubungkan penyedia makanan berlebih dengan pembeli melalui katalog interaktif, autentikasi berbasis peran, dan alur transaksi terintegrasi.

**Developed By:** Chofifah Humayra

---

## URL Aplikasi

- **Produksi (Cloud / Render):** `https://NAMA-LAYANAN-ANDA.onrender.com/#/` *(ganti setelah deployment Langkah 13 selesai)*
- **Build Lokal (Single Origin):** `http://127.0.0.1:3000/#/`
- **Pengembangan Lokal (Vite Dev):** `http://127.0.0.1:5173/#/`

---

## Teknologi yang Digunakan

- **Frontend:** Vue 3, Vue Router (`createWebHashHistory`), Vite
- **Backend:** Node.js (`>=22`, direkomendasikan lini 24 `>=24.12.0`), Express 5, `jsonwebtoken` (JWT Bearer 15 menit), `bcryptjs`, `helmet`, `express-rate-limit`
- **Database & Pengolahan Media:** PostgreSQL (driver `pg` dengan TLS) dan `sharp` (validasi serta konversi foto penawaran ke format WebP)
- **Deployment & Cloud:** Render (Free Web Service) dan Neon (Free PostgreSQL)

---

## Capaian Pengembangan

### Modul 10 — Integrasi Full-Stack Vue & REST API
- **Integrasi End-to-End:** Menghubungkan antarmuka komponen Vue 3 dengan backend REST API Express dan basis data PostgreSQL.
- **Autentikasi & Sesi:** Menerapkan pendaftaran mandiri (pembeli dan penyedia), manajemen sesi berbasis JWT di memori, serta perlindungan route via *navigation guards*.
- **Manajemen Penawaran & Foto:** Fitur CRUD penawaran milik penyedia dengan unggah foto opsional (konversi WebP via `sharp`) dan pencegahan konflik edisi (*optimistic concurrency control* via versi DTO).
- **Alur Transaksi & Stok:** Pemesanan makanan, reservasi dan pemulihan stok otomatis, pembatalan/penolakan dengan alasan, serta pencatatan serah terima (berbayar maupun gratis di tempat).
- **Dashboard Agregat:** Menampilkan metrik analitik bisnis sesuai peran akun (total belanja, pendapatan, penghematan, dan unit tersalurkan).

### Modul 11 — Pengujian & Deployment Publik
- **Single Origin Build:** Menyajikan hasil kompilasi statis Vue (`frontend/dist`) dan endpoint REST API (`/api`) dalam satu origin melalui Express.
- **Pemisahan Lingkungan & TLS:** Memisahkan konfigurasi lokal (`.env`, `PGSSL=disable`, `TRUST_PROXY_HOPS=0`) dan konfigurasi cloud (`PGSSL=require`, `TRUST_PROXY_HOPS=1`).
- **Inisialisasi Skema Cloud Tanpa Seed:** Menerapkan `database/11_schema_cloud.sql` dan `database/12_alur_transaksi.sql` dalam satu transaksi atomik pada database Neon kosong.
- **Pengujian & Audit Kualitas:** Melaksanakan pengujian otomatis HTTP deployment (`deploy:test`), pengujian regresi dan konkurensi (`workflow:test`), pemeriksaan aksesibilitas keyboard/WCAG 2.2, serta pengukuran performa build.

---

## Prasyarat & Konfigurasi Lingkungan

- **Node.js:** `^22.18.0` atau `>=24.12.0`
- **PostgreSQL:** v14.x atau lebih baru (lokal) serta akun Neon Free (cloud)
- **Editor:** Visual Studio Code

### 1. Variabel Lingkungan Lokal (`.env`)
Salin `.env.example` menjadi `.env` di root proyek untuk pengembangan dan pengujian build lokal:

```env
PGHOST=127.0.0.1
PGPORT=5432
PGDATABASE=sisabaik_dev
PGUSER=postgres
PGPASSWORD=password_postgresql_lokal
PGSSL=disable
JWT_SECRET=isi_64_digit_hex_acak_lokal
NODE_ENV=development
HOST=127.0.0.1
PORT=3000
TRUST_PROXY_HOPS=0
```

### 2. Variabel Lingkungan Cloud (`.env.cloud` & Dashboard Render)
Salin `.env.cloud.example` menjadi `.env.cloud` secara privat di perangkat lokal untuk menjalankan perintah inisialisasi dan verifikasi cloud (jangan di-commit ke Git):

```env
PGHOST=ep-nama-host-anda.region.aws.neon.tech
PGPORT=5432
PGDATABASE=neondb
PGUSER=role_neon_anda
PGPASSWORD=password_neon_anda
PGSSL=require
CLOUD_CONFIRM_DATABASE=neondb
```

*(Pada dashboard Render Web Service, tambahkan juga `NODE_ENV=production`, `NODE_VERSION=24`, `HOST=0.0.0.0`, `TRUST_PROXY_HOPS=1`, dan `JWT_SECRET` 64 digit hex acak khusus cloud).*

---

## Perintah Menjalankan Aplikasi

Instalasi dependensi (root dan frontend):
```bash
npm ci
npm --prefix frontend ci --include=dev
```

### Mode Pengembangan (Dua Terminal)
```bash
# Terminal 1 (Backend API di port 3000)
npm run dev

# Terminal 2 (Frontend Vite di port 5173)
npm --prefix frontend run dev
```

### Mode Build Produksi Lokal (Single Origin Port 3000)
```bash
# Membangun berkas statis Vue ke frontend/dist
npm run build

# Menjalankan Express yang menyajikan build Vue dan API sekaligus
npm run start:local
```

### Mode Produksi Cloud (Render)
```bash
npm start
```

### Inisialisasi & Migrasi Database Cloud (Neon)
```bash
# Inisialisasi awal database Neon yang masih kosong (tanpa seed)
npm run db:init:cloud

# Migrasi jika tabel sudah ada sebelumnya (tanpa reset data)
npm run db:migrate:cloud
```

---

## Alur Pendaftaran dan Peninjauan Usaha

1. **Pendaftaran Mandiri:** Pengguna mendaftar melalui halaman `/#/daftar` dengan memilih peran **Pembeli** atau **Penyedia** serta kata sandi sendiri (minimal 15 karakter, maksimal 72 byte UTF-8).
2. **Status Awal Penyedia:** Akun penyedia yang baru mendaftar otomatis berstatus `menunggu` dan belum dapat membuat penawaran makanan.
3. **Verifikasi Pengelola via CLI:** Pengelola atau dosen meninjau profil usaha penyedia melalui terminal root:
   ```bash
   # Verifikasi pada database lokal
   npm run penyedia:verifikasi email_penyedia@contoh.com

   # Verifikasi pada database cloud (Neon)
   npm run penyedia:verifikasi:cloud email_penyedia@contoh.com
   ```
   *(Tambahkan flag `--tolak` di akhir perintah apabila profil usaha ditolak).*
4. **Pembaruan Status di Antarmuka:** Penyedia membuka halaman **Profil usaha** (`/#/akun/penyedia`) dan menekan tombol **Periksa status** untuk mengaktifkan akses pengelolaan penawaran.

---

## Definisi Metrik Bisnis & Dampak

- **`unitDipesan` & `nilaiPemesanan`:** Total kuantitas dan nilai harga snapshot dari pesanan yang tidak dibatalkan (tahap reservasi belum dihitung sebagai penerimaan/belanja final).
- **`unitTersalurkan`:** Jumlah kuantitas unit makanan dari pesanan berstatus `selesai` yang telah tercatat diambil (`status = diambil` dan `diambil_pada` terisi). Angka ini merepresentasikan jumlah unit/paket, bukan jumlah individu unik maupun satuan berat (kg).
- **`totalBelanja` (Pembeli) & `pendapatanDiterima` (Penyedia):** Akumulasi nilai transaksi dari pesanan yang memenuhi syarat `selesai`, pengambilan `diambil`, dan pembayaran `dibayar` atau `gratis`.
- **`penghematanPembeli` / `diskonDiberikan`:** Selisih antara total nilai harga normal snapshot dan total nilai transaksi pada pesanan yang selesai dan lunas.
- **`penghematanBiayaPenjual`:** Bernilai `null` (belum dihitung karena sistem tidak mengumpulkan data biaya produksi maupun biaya pembuangan limbah usaha).
- **`jumlahPenawaran`, `penawaranAktif`, & `stokTersedia`:** Dihitung khusus berdasarkan data penawaran milik akun penyedia yang bersangkutan.

---

## Batasan Fitur & Layanan

- **Metode Pembayaran:** Pembayaran dilakukan langsung di tempat saat pengambilan pesanan atau gratis (`Rp0`); belum tersedia integrasi *payment gateway* daring.
- **Administrasi Verifikasi:** Persetujuan akun penyedia dilakukan melalui CLI pengelola; belum tersedia dashboard admin berbasis web maupun verifikasi email otomatis.
- **Manajemen Sesi:** Token JWT disimpan hanya di memori antarmuka (*in-memory*) untuk keamanan, sehingga memuat ulang halaman (*reload*) akan menghapus sesi dan mengharuskan pengguna login kembali.
- **Keterbatasan Layanan Gratis:** Render Free akan memasuki mode tidur (*sleep*) setelah 15 menit tanpa aktivitas dan memiliki penyimpanan lokal sementara. Seluruh data transaksi dan foto penawaran (WebP) disimpan secara persisten di PostgreSQL Neon.
- **Konteks Data:** Seluruh akun dan transaksi pada repositori ini merupakan simulasi pengujian perangkat lunak dan bukan klaim dampak ekonomi maupun lingkungan nyata.

---

## Langkah Pengujian

1. **Pemeriksaan HTTP Deployment (10 Pemeriksaan Non-Destruktif):**
   ```bash
   # Uji build lokal
   npm run deploy:test [http://127.0.0.1:3000](http://127.0.0.1:3000)

   # Uji layanan publik Render
   npm run deploy:test [https://NAMA-LAYANAN-ANDA.onrender.com](https://NAMA-LAYANAN-ANDA.onrender.com)
   ```
2. **Pengujian Regresi Transaksi, Otorisasi, dan Konkurensi Lokal:**
   Pastikan server lokal berjalan (`npm run start:local`), lalu jalankan pada terminal terpisah:
   ```bash
   npm run workflow:test
   ```
3. **Dokumentasi Bukti Pengujian:**
   Seluruh matriks pengujian fungsional (`F01`–`F20`), pengujian keamanan akses (`S01`–`S11`), pemeriksaan aksesibilitas keyboard/WCAG 2.2, audit performa build, potongan log yang telah disamarkan, serta refleksi proyek tersimpan di folder `docs/minggu12`.