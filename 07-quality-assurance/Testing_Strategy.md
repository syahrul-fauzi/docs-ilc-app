# 🧪 Testing Strategy: ILC-APP

## 🎯 Level Pengujian
1. **Unit Testing**: Menggunakan `Jest` untuk helper functions dan business logic.
2. **Component Testing**: Menggunakan `React Native Testing Library` untuk Ag-UI components.
3. **E2E Testing**: Menggunakan `Maestro` atau `Detox` untuk alur kritis (Login, AI Ask, Consultation).

### 3. Keamanan & Audit (Security Scan)
- **NPM Audit**: Mengecek dependensi dari kerentanan keamanan (High/Critical).
- **Leak Detection**: Pencarian otomatis untuk API Keys atau Secrets yang tidak sengaja ter-commit di kode sumber.
- **SSL Pinning**: Direkomendasikan untuk komunikasi API di lingkungan produksi.

## Integrasi CI/CD (GitHub Actions)

Proyek ILC-APP menggunakan alur kerja otomatis di `.github/workflows/ilc-app-ci.yml`:
1. **Security Audit**: Langkah pertama untuk memastikan kode aman dan dependensi bersih.
2. **Unit Tests**: Menjalankan seluruh suite Jest dengan cakupan (coverage) minimal 90%.
3. **E2E Tests**: Menjalankan Maestro flows di `macos-latest` runner untuk validasi aplikasi di simulator.
4. **Reporting**: Hasil pengujian diunggah sebagai artifacts untuk tinjauan tim.

## 🏁 Maestro E2E Flows

Proyek ini memiliki suite pengujian E2E yang komprehensif menggunakan Maestro:

- **auth.yaml**: Alur login dan registrasi berhasil.
- **auth_failure.yaml**: Validasi input dan pesan kesalahan saat login gagal.
- **ai_search.yaml**: Alur pencarian hukum menggunakan AI dan verifikasi Trust Signals.
- **billing.yaml**: Simulasi pembayaran, pemilihan paket, dan riwayat transaksi.
- **community.yaml**: Interaksi di feed komunitas (posting, like, dan switching tabs).
- **profile.yaml**: Manajemen profil, perubahan pengaturan, dan logout.
- **network_timeout.yaml**: Pengujian ketahanan aplikasi saat koneksi API lambat atau terputus.

Jalankan suite lengkap dengan:
```bash
maestro test maestro/suite.yaml
```

## 📊 Status Pengujian Terkini (Update 2026-01-12)

Seluruh suite pengujian saat ini dalam status **PASS (100%)** dengan detail sebagai berikut:
- **Total Test Suites**: 24
- **Total Tests**: 131
- **Key Achievements**:
  - Resolusi masalah `Y.UndoManager` pada `LegalEditorService`.
  - Implementasi mocking yang stabil untuk modul Expo (`expo-device`, `expo-notifications`, `expo-secure-store`).
  - Validasi alur **Agentic Continuous Learning** dengan sinkronisasi memori asinkron.
  - Perbaikan sinkronisasi `BillingService` pada simulasi E2E lifecycle.

## 🛠️ Konfigurasi Teknis (React 19 & Expo 52+)

Proyek ini menggunakan React 19 yang memerlukan konfigurasi khusus untuk Jest dan React Native Testing Library (RNTL).

### Setup Environment
- **Library**: `@testing-library/react-native` v13.3.3+ (mendukung React 19).
- **Preset**: `jest-expo` v54.
- **Mocks**:
  - `react-native`: Mocking komponen host (`View`, `Text`, `FlatList`) menggunakan `string` atau `React.createElement` untuk kompatibilitas RNTL.
  - `react-native-reanimated`: Mock global di `jest.setup.js` untuk menghindari native module errors.
  - `nativewind`: Mock styling engine.

### Common Issues & Solutions

#### 1. Maximum Call Stack Size Exceeded
Terjadi karena circular dependency saat melakukan `jest.requireActual('react-native')` di dalam file test yang sudah memiliki mock `react-native`.
**Solusi**: Gunakan mock eksplisit untuk `react-native` di awal file test atau andalkan mock global di `jest.setup.js`.

#### 2. NativeAnimatedModule.apply Error
Terjadi saat pengujian komponen yang menggunakan `Animated` atau `reanimated` selama fase cleanup.
**Solusi**: Tambahkan mock untuk `NativeAnimatedModule` di dalam `NativeModules`:
```tsx
NativeModules.NativeAnimatedModule = {
  startOperationBatch: jest.fn(),
  finishOperationBatch: jest.fn(),
  createAnimatedNode: jest.fn(),
  // ... mock methods lainnya
  getValue: jest.fn((tag, cb) => cb && cb(0)),
};
```

#### 3. Alert Mocking
Untuk memverifikasi `Alert.alert`, pastikan `Alert` di-mock di `react-native` dan di-import dengan benar di file test untuk asersi.
```tsx
import { Alert } from 'react-native';
// ...
expect(Alert.alert).toHaveBeenCalledWith("Judul", "Pesan", expect.any(Array));
```
