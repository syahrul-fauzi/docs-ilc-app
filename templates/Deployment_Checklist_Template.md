# Deployment Checklist — ILC-APP

Gunakan checklist ini sebelum melakukan rilis ke staging atau production untuk memastikan kualitas dan stabilitas aplikasi.

## 1. Pre-Deployment (Development Readiness)
- [ ] **Linting & Type Checking**: Jalankan `npm run lint` dan `npx tsc` tanpa error.
- [ ] **Unit Tests**: Jalankan `npm test` dan pastikan coverage minimal 80%.
- [ ] **DDD/FSD Alignment**: Verifikasi tidak ada circular dependencies antar features.
- [ ] **Environment Variables**: Pastikan `.env.production` sudah terisi dengan API Keys yang benar.

## 2. Expo & Native Configuration
- [ ] **app.json / app.config.js**:
    - [ ] Versi aplikasi (`version` & `buildNumber`/`versionCode`) sudah ditingkatkan.
    - [ ] Bundle Identifier (iOS) dan Package Name (Android) sudah sesuai.
    - [ ] `newArchEnabled` diatur sesuai target (default: true).
- [ ] **Assets**: Pastikan icon, splash screen, dan adaptive icons sudah teroptimasi.
- [ ] **Permissions**: Verifikasi izin akses (Kamera, Notifikasi, Storage) sudah dideklarasikan dengan benar.

## 3. API & Backend Integration
- [ ] **SSL Pinning**: Verifikasi sertifikat API sudah terbaru.
- [ ] **Sentry / Bugsnag**: Pastikan integrasi monitoring error aktif dan sourcemaps sudah terupload.
- [ ] **Analytics**: Verifikasi event-event kritis (Login, Ask AI, Payment) terlacak dengan benar.

## 4. Build & Distribution (EAS)
- [ ] **Staging Build**: `eas build --profile staging`.
- [ ] **Production Build**: `eas build --profile production`.
- [ ] **Submission**: `eas submit` ke Google Play Store / Apple App Store.
- [ ] **OTA Updates**: Jika menggunakan Expo Updates, jalankan `eas update` untuk perbaikan cepat.

## 5. Post-Deployment Validation
- [ ] **Smoke Test**: Verifikasi fitur utama (Ask AI, Community Feed, Consultation) berjalan di device fisik.
- [ ] **Deep Links**: Pastikan navigasi via URL scheme / Universal Links berfungsi.
- [ ] **Performance Check**: Pantau startup time dan penggunaan memory via Firebase Performance atau Sentry.

---
*Dibuat oleh: ILC Super Agent*
