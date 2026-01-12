# ⚛️ React 19 Compatibility Tracking (ILC-APP)

Dokumen ini melacak status kompatibilitas React 19 dalam proyek ILC-APP, termasuk *workarounds* yang diterapkan dan rencana migrasi ke depan.

## Status Saat Ini
- **Versi React**: 19.2.3
- **Versi Expo**: 54.0.0 (SDK 54)
- **Status Test Runner**: Terkonfigurasi dengan penyesuaian untuk React 19.

## Daftar Workarounds (Current)

### 1. Mocking Host Components (Jest)
React 19 mengubah cara internal rendering yang menyebabkan kegagalan pada `react-test-renderer` jika komponen native tidak di-mock dengan benar.
- **Solusi**: Menggunakan string-based host component references atau `React.createElement` secara manual di `jest.setup.js` dan unit tests.
- **File Terkait**: `jest.setup.js`, `src/app/__tests__/consult.test.tsx`, `src/app/__tests__/ask.test.tsx`.

### 2. Peer Dependencies (`legacy-peer-deps`)
Beberapa library pihak ketiga (seperti `nativewind` atau `recoil`) mungkin belum secara resmi mendukung React 19 di `package.json`.
- **Solusi**: Menggunakan flag `--legacy-peer-deps` saat instalasi jika terjadi konflik dependensi.

### 3. useEffect Cleanup
React 19 lebih ketat dalam siklus hidup komponen, yang dapat menyebabkan `useEffect` cleanup berjalan lebih awal dalam lingkungan testing.
- **Solusi**: Menggunakan guard `isMounted` di dalam `useEffect` async operations.

## Rencana Migrasi & Monitoring (Migration Plan)

### 1. Pemantauan Berkala (Regular Reviews)
- **Jadwal**: Setiap 2 minggu (bi-weekly) pada hari Senin.
- **PIC**: Senior Mobile Engineer.
- **Metode**: Audit `npm outdated` dan memantau rilis di repository GitHub React Native, Expo, dan NativeWind.

### 2. Strategi Pembaruan Dependensi (Dependency Updates)
- **Priority 1**: `react-native` (Target 0.77+).
- **Priority 2**: `@testing-library/react-native` (Versi yang mendukung React 19 secara native).
- **Priority 3**: Library UI (`nativewind`, `lucide-react-native`).
- **Langkah**:
  1. Buat branch baru `migration/react-19-native`.
  2. Jalankan `npm install <package>@latest --legacy-peer-deps`.
  3. Uji fungsionalitas dasar di simulator Android dan iOS.

### 3. Modifikasi Kode (Code Modifications)
- **Refactoring Mocks**: Migrasi dari string-based mocks ke standard RNTL queries setelah library diperbarui.
- **Standardisasi useEffect**: Terapkan pola `isMounted` atau `AbortController` secara konsisten di seluruh service layer.
- **Strict Mode**: Aktifkan React Strict Mode di `_layout.tsx` untuk mendeteksi *deprecated patterns*.

### 4. Persyaratan Pengujian (Testing Requirements)
- **Unit Test**: 100% pass rate untuk seluruh suite Jest.
- **E2E Test**: Seluruh Maestro flows (`auth`, `billing`, `ai_search`) wajib lulus di Android dan iOS.
- **Performance Audit**: Pastikan tidak ada regresi pada frame rate (FPS) saat rendering list besar (search results).

## Log Perubahan
- **2026-01-12**: Inisialisasi dokumen tracking, penerapan mock manual untuk `consult.test.tsx` dan `ask.test.tsx`, penyusunan rencana migrasi detail, aktivasi `React.StrictMode` di `_layout.tsx`, dan audit awal komponen UI (`Input`, `Button`).
- **2026-01-12 (Update)**: Validasi integrasi `BillingRepository` dengan `apiClient` untuk penanganan state aman, finalisasi Maestro test suite dengan cakupan 100% layar profil baru, dan standardisasi komponen UI (Spinner, Text, Card) untuk konsistensi rendering React 19.
- **2026-01-12 (Finalize)**: Refactoring menyeluruh layar Edit Profil, Notifikasi, Riwayat Transaksi, dan Langganan untuk kepatuhan penuh terhadap desain sistem atomik dan reliabilitas pengujian E2E. Verifikasi alur navigasi Maestro menggunakan `testID` yang seragam.
