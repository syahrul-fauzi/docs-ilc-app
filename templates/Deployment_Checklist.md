# Deployment Checklist — ILC-APP

Daftar verifikasi sebelum melakukan rilis aplikasi ke Staging atau Production.

## 1. Verifikasi Kode
- [ ] Linter lulus (tidak ada error/warning kritis).
- [ ] Seluruh unit test lulus (`npm test`).
- [ ] Code coverage minimal 80%.
- [ ] Tidak ada hardcoded API keys atau sensitive data.

## 2. Konfigurasi Environment
- [ ] Versi aplikasi di `app.json` sudah diupdate.
- [ ] Base URL API mengarah ke environment yang benar.
- [ ] API Keys (OpenAI, Maps, dll) sudah menggunakan production key (jika ke prod).

## 3. Aset & Resource
- [ ] Splash screen dan icon aplikasi sudah sesuai.
- [ ] Seluruh aset gambar sudah dioptimasi ukurannya.

## 4. Testing Manual (Smoke Test)
- [ ] Login/Register berhasil.
- [ ] Fitur Tanya AI memberikan respon.
- [ ] Feed Komunitas dapat dimuat.
- [ ] Notifikasi masuk (jika ada).

## 5. Rilis
- [ ] Build artifact (APK/IPA/AAB) berhasil dibuat tanpa error.
- [ ] Changelog sudah diperbarui.
- [ ] Tag versi di Git sudah dibuat.
