# Troubleshooting: Tab Menu Content Display Issues

Dokumen ini mencatat masalah dan solusi terkait tampilan konten pada tab menu di ILC-APP.

## Masalah: Konten Tab Tidak Muncul (Hanya Menu Tab)

### 1. Error Hidrasi (Hydration Error) pada Platform Web
- **Gejala**: Konsol browser menunjukkan error `In HTML, %s cannot be a child of <%s>`.
- **Penyebab**: Komponen `Text` dengan varian heading (`h1`-`h6`) secara otomatis menyetel `role="heading"`. Jika induknya memiliki `accessibilityRole="header"`, ini menyebabkan elemen heading bersarang (nested) yang tidak valid di HTML.
- **Solusi**: Hapus `accessibilityRole="header"` dari komponen induk `View` jika menggunakan `Text` varian heading di dalamnya.
- **File Terkait**: 
    - `src/app/(tabs)/chat.tsx`
    - `src/app/(tabs)/search.tsx`
    - `src/app/(tabs)/index.tsx`

### 2. Kebijakan CORS (Cross-Origin Resource Sharing)
- **Gejala**: Request API ke `localhost:3001` diblokir oleh browser.
- **Penyebab**: Origin frontend (`http://localhost:8081`) belum didaftarkan di backend.
- **Solusi**: Tambahkan `http://localhost:8081` ke dalam `allowedOrigins` di konfigurasi backend.
- **File Terkait**:
    - `apps/api/src/main.ts`

### 3. Kegagalan Otentikasi pada Mock Mode
- **Gejala**: Request API mengembalikan status 401 atau error terkait token.
- **Penyebab**: Token yang dihasilkan secara dinamis di `UserRepository` tidak konsisten dengan ekspektasi backend saat berjalan dalam mode pengembangan.
- **Solusi**: Gunakan token statis (`mock-token`) untuk mempermudah pengembangan dan pengujian lokal.
- **File Terkait**:
    - `src/entities/user/repository/UserRepository.ts`

## Monitoring dan Verifikasi
- Gunakan `npm run web -- --port 8081` untuk menjalankan frontend.
- Pastikan backend API aktif dan mengembalikan data (cek via `curl` atau browser).
- Verifikasi melalui **OpenPreview** untuk memastikan tidak ada error konsol yang menghambat rendering.

---
*Terakhir Diperbarui: 2026-01-16*
