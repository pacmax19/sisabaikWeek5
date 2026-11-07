## Integrasi Chapter 11 — Integrasi Full Stack

### Konfigurasi & Lingkungan Pengembangan
- **Versi Node.js:** Node.js v18+ / v20+
- **Jalur Lokal:**
  - Backend Dev: `http://127.0.0.1:3000`
  - Frontend Dev: `http://127.0.0.1:5173`
  - Frontend Preview: `http://127.0.0.1:4173`
  - Production Build (Single-Origin): `http://127.0.0.1:3000`
- **Proxy Vite:** Target `/api` diteruskan ke `http://127.0.0.1:3000`

### Fitur Alur Transaksi & Sistem
- **Autentikasi & Sesi:** Registrasi mandiri akun pembeli dan penyedia. Sesi dikelola secara *in-memory* via Vue Reactive (token hilang saat *refresh* browser).
- **Peninjauan Usaha:** Akun penyedia baru berstatus `menunggu` dan memerlukan pembaruan status `terverifikasi` di basis data sebelum mempublikasikan penawaran.
- **Payload & Concurrency:** Payload penawaran mendukung foto (Max 3MB, Base64/DataURL) dan kolom `versi` untuk penanganan *optimistic concurrency lock* saat update data.
- **Stok & Pengambilan:** Stok server otomatis berkurang saat pesanan dibuat dan pulih (*restock*) secara otomatis jika pesanan dibatalkan. Pembayaran dilakukan di tempat (*Cash on Delivery*).
- **Metrik Dashboard:** Menghitung total ringkasan pesanan dan pendapatan tanpa memasukkan reservasi/pesanan menggantung.

### Batasan Sistem Aktual
- Sesi autentikasi tersimpan *in-memory*.
- Belum terintegrasi *Payment Gateway*, *Reset Password*, atau *Email Verification*.
- Belum menerapkan *Idempotency Key*, *Realtime WebSockets*, maupun metrik penghematan biaya penjual.

### Hasil Pengujian Automasi
- **Workflow Testing:** 26/26 skenario alur transaksi lulus (`npm run workflow:test`).