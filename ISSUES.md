# 📋 Daftar Permasalahan Teridentifikasi (ILC-APP)

## 🔴 Prioritas Tinggi (Critical)

### 1. Expo Router LinkingContext Context Error
- **Status**: ✅ FIXED
- **Deskripsi**: Aplikasi terkadang gagal menemukan context linking saat navigasi dalam.
- **Solusi**: Restrukturisasi hierarki provider di `_layout.tsx` menjadi `AppProviders` (non-router) dan `NavigationStack` (router-dependent).

### 2. Keamanan Data (PII Masking)
- **Status**: ✅ FIXED
- **Deskripsi**: Data pribadi pengguna (PII) berisiko terkirim ke LLM eksternal dalam bentuk teks mentah.
- **Solusi**: Implementasi Axios interceptor di `apiClient.ts` dan pre-flight check di `AIRepository.ts` menggunakan utilitas `piiMasking.ts`.

---

## 🟡 Prioritas Menengah (Medium)

### 3. Sinkronisasi Backend (404 Endpoints)
- **Status**: ✅ FIXED
- **Deskripsi**: Beberapa fitur (Community Feed, Chat History, Case Detail, Comments, Staging Promote) mendapatkan respon 404 dari API.
- **Solusi**: Registrasi modul `CommunityModule` dan `ChatModule` di `AppModule` serta melengkapi missing endpoints di `CommunityController` dan `StagingController`.

### 4. Manajemen Memori Log
- **Status**: ✅ FIXED
- **Deskripsi**: Logger menyimpan 2000 entri di memori, berisiko memory leak pada mobile.
- **Solusi**: Reduksi `MAX_LOGS` menjadi 500 entri untuk mengurangi tekanan memori.

### 5. Integration Timeout (LegalDatabase)
- **Status**: ✅ FIXED
- **Deskripsi**: Integrasi `LegalDatabase` (JDIH) sering mengalami timeout.
- **Solusi**: Peningkatan timeout menjadi 30 detik dan penambahan mekanisme retry (5x) pada `IntegrationService`.

---

## 🟢 Prioritas Rendah (Low)

### 5. Inkonsistensi Dark Mode pada Web
- **Status**: Fixed (Pending Verification)
- **Deskripsi**: Dark mode terkadang tidak sinkron antara native dan web.
- **Dampak**: Pengalaman visual pengguna kurang optimal.
- **Rencana Perbaikan**: Sudah diperbaiki via `StyleSheet.setFlag('darkMode', 'class')`. Perlu pengujian regresi.
