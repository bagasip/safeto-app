# SAFETO Deploy Ready (Render)

Paket ini menyiapkan konfigurasi deployment ke Render untuk frontend statis dan API Node.js. **Paket ini belum dipublikasikan ke internet** karena deployment membutuhkan akun hosting dan repository Git yang Anda kendalikan.

## Cara deploy
1. Ekstrak ZIP dan unggah folder proyek ke repository GitHub baru (misalnya `safeto-deploy-ready`).
2. Login ke Render, pilih **New + → Blueprint**, hubungkan repository tersebut, lalu deploy `render.yaml`.
3. Render akan membuat dua service: `safeto-api` dan `safeto-web`. Tunggu keduanya aktif.
4. Buka URL `safeto-api` dan pastikan `/health` menampilkan `ok: true`.
5. Buka URL `safeto-web`. Masuk Pengaturan, isi API Base URL dengan `https://URL-SAFETO-API.onrender.com/api/v1`, simpan, pilih API mode, lalu login.

## Batasan dan keamanan
- API menggunakan JSON file di persistent disk, bukan PostgreSQL. Ini hanya tahap pilot/preview; bukan arsitektur produksi skala besar.
- `CORS_ORIGIN` diset `*` untuk memudahkan preview awal. Sebelum produksi, ubah ke URL frontend yang persis, misalnya `https://safeto-web.onrender.com`.
- Seed akun demo (`admin@safeto.test`) dibuat oleh backend saat file data pertama kali dibuat. Ganti/hapus kredensial demo sebelum publikasi kepada pengguna nyata. Karena akun seed memakai password demo tetap, jangan menerima data sensitif atau trafik publik sebelum proses bootstrap admin yang aman dibuat.
- SOS hanya tercatat di aplikasi; tidak menghubungi polisi/ambulans/kontak darurat.
- Pembayaran hanya membuat catatan pending; belum terhubung ke payment gateway.
- Tracking GPS real-time, push notifications, KYC dan pengujian keamanan independen belum tersedia.
- Simpan rahasia JWT hanya di environment variables hosting, bukan di repository.

## Menjalankan lokal
Backend: `cd backend && npm install && npm start`
Frontend: `cd frontend && python3 -m http.server 3000`
