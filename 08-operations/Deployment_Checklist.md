# 🚀 Deployment Checklist & Release Guide
> **ILC-APP (Indonesia Lawyers Club)**  
> Versi: 1.0.0 (Initial Release)

Checklist ini dirancang untuk memastikan deployment **ILC-APP** berjalan lancar, aman, dan memenuhi standar kualitas produksi.

---

## 📋 1. Pre-Deployment Validation (Staging)

### ✅ Code Quality & Security
- [ ] **Linting & Formatting**: Jalankan `npm run lint` dan pastikan tidak ada error.
- [ ] **Type Checking**: Jalankan `npm run type-check` (tsc) tanpa error.
- [ ] **Unit Tests**: Coverage minimal 80%. Jalankan `npm test`.
- [ ] **Security Scan**: Audit dependensi dengan `npm audit`.
- [ ] **Secrets Check**: Pastikan tidak ada API Key atau kredensial yang ter-commit (gunakan `.env`).

### ✅ Fungsionalitas Utama (Smoke Test)
- [ ] **Auth Flow**: Login, Register, Logout, Session Expiry.
- [ ] **AI Search**: Query hukum mengembalikan hasil dengan *Trust Signals* valid.
- [ ] **Community**: Feed memuat, Posting berhasil, Komentar berfungsi.
- [ ] **Legal Tools**: Editor dokumen bisa dibuka, diedit, dan menyimpan perubahan.
- [ ] **Billing**: Simulasi pembayaran (Sandbox) berhasil.

### ✅ UI/UX & Responsiveness
- [ ] **Safe Area**: Tampilan tidak terpotong notch/dynamic island.
- [ ] **Keyboard Handling**: Input tidak tertutup keyboard (KeyboardAvoidingView).
- [ ] **Loading States**: Skeleton loading atau spinner muncul saat fetch data.
- [ ] **Error Handling**: Error network menampilkan pesan yang ramah pengguna (Toast/Alert).

---

## 🏗️ 2. Build Preparation (Expo EAS)

### 📱 Konfigurasi App (app.json)
- [ ] **Version Code**: Update `version` dan `android.versionCode` / `ios.buildNumber`.
- [ ] **App Icon**: Pastikan ikon resolusi tinggi tersedia.
- [ ] **Splash Screen**: Tampilan splash screen sesuai branding.
- [ ] **Deep Links**: Skema URL (`ilc-app://`) terdaftar dan berfungsi.
- [ ] **Permissions**: Deskripsi izin (Camera, Location) jelas dan sopan.

### 🔐 Environment Variables
- [ ] **Production API URL**: Point ke server production (`https://api.indonesialawyersclub.id`).
- [ ] **Analytics Keys**: Mixpanel/Google Analytics token untuk production.
- [ ] **Sentry DSN**: Untuk error tracking production.

### 📦 Build Command
```bash
# Login ke Expo
eas login

# Cek kesehatan proyek
npx expo-doctor

# Build untuk Production (Android Bundle & iOS IPA)
eas build --profile production --platform all
```

---

## 🚀 3. Release & Submission

### 🤖 Android (Google Play Store)
- [ ] **Upload AAB**: Upload file `.aab` ke Play Console (Track: Production atau Open Testing).
- [ ] **Store Listing**: Update deskripsi, screenshot, dan "What's New".
- [ ] **Content Rating**: Pastikan kuesioner rating konten terisi.
- [ ] **Privacy Policy**: Link kebijakan privasi aktif dan valid.

### 🍎 iOS (App Store Connect)
- [ ] **Upload Build**: Submit via Transporter atau EAS Submit.
- [ ] **TestFlight**: Distribusikan ke internal tester untuk validasi akhir.
- [ ] **App Review Info**: Sediakan akun demo untuk reviewer Apple.
- [ ] **Compliance**: Konfirmasi penggunaan enkripsi (jika ada).

---

## 📡 4. Post-Deployment Monitoring

### 📊 Real-time Monitoring
- [ ] **Error Rates**: Pantau Sentry untuk crash mendadak.
- [ ] **API Latency**: Cek response time di dashboard backend.
- [ ] **User Signups**: Validasi flow registrasi user baru di production.

### 🔄 Rollback Plan
Jika terjadi *Critical Bug* (Severity 1):
1.  **Immediate Hotfix**: Perbaiki kode -> `eas update --branch production`.
2.  **Server-side Toggle**: Matikan fitur bermasalah via Remote Config (jika ada).
3.  **App Store Rollback**: Tidak bisa instan, gunakan *Expedited Review* untuk update darurat.

---

## 📝 Catatan Rilis (Changelog)

### v1.0.0 - Initial Release
- **Fitur Baru**: AI Legal Assistant, Community Feed, Document Editor.
- **Perbaikan**: Optimasi performa startup.
- **Keamanan**: Enkripsi end-to-end untuk konsultasi.

---
*Dibuat otomatis oleh Trae AI Assistant*
