# SisaBaik

SisaBaik adalah proyek berkembang pada mata kuliah Pengembangan Web. Aplikasi ini dirancang untuk membantu penyedia memulihkan nilai stok makanan berlebih melalui penjualan dengan harga khusus atau penyaluran, sekaligus membantu masyarakat memperoleh makanan yang lebih terjangkau dan mengurangi limbah pangan.

## Capaian Chapter 7

- Membangun REST API menggunakan Express.js yang terhubung ke basis data PostgreSQL (`sisabaik_dev`).
- Mengimplementasikan operasi CRUD penuh pada entitas `penawaran` dan modul transaksi pembuatan `pesanan`.
- Menggunakan transaksi PostgreSQL (`BEGIN`, `COMMIT`, `ROLLBACK`) untuk memastikan konsistensi stok dan mencegah race condition saat pemesanan beruntun.
- Menerapkan validasi input yang ketat pada layer aplikasi (termasuk penanganan ID berformat string dan pencegahan SQL Injection).
- Menangani error penanganan protokol HTTP sesuai standar (`400 Bad Request`, `404 Not Found`, `409 Conflict`, `413 Payload Too Large`, `415 Unsupported Media Type`, dan `500 Internal Server Error`).
- Memperbarui kontrak payload request dari `namaPemesan` menjadi `emailPembeli`.

## Prasyarat & Lingkungan

- Node.js: v18.x atau lebih baru
- PostgreSQL: v14.x atau lebih baru
- Basis data `sisabaik_dev` sudah dikonfigurasi dan diisi dengan skema basis data serta data awal (seed) dari Chapter 6.
- Berkas `.env` telah dikonfigurasi sesuai pengaturan koneksi basis data lokal.

## Cara Menjalankan Aplikasi

1. Pastikan PostgreSQL service sudah berjalan dan database `sisabaik_dev` sudah siap.
2. Jalankan server pengembangan:
   ```bash
   npm run dev

## Integritas akademik

Pengerjaan proyek berkembang mengikuti kebijakan mata kuliah . AI generatif tidak diperkenankan pada tahap ini. Mahasiswa wajib mampu menjelaskan setiap elemen dan atribuy yang digunakan.