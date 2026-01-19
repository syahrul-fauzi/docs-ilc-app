# 🚀 Panduan Deployment Staging - ILC-APP

Dokumen ini menjelaskan prosedur deployment ke lingkungan staging untuk verifikasi internal dan uji coba oleh tim legal.

## 1. Persiapan Lingkungan
Lingkungan staging menggunakan konfigurasi yang mendekati produksi namun dengan basis data terisolasi.

### Environment Variables (Staging)
Dikonfigurasi di `eas.json` (Profile: `staging`):
- `APP_ENV`: `staging`
- `EXPO_PUBLIC_API_URL`: `https://staging-api.indonesialawyersclub.id`
- `EXPO_PUBLIC_SOCKET_URL`: `https://staging-socket.indonesialawyersclub.id`
- `EXPO_PUBLIC_TENANT_ID`: `ilc-staging`

## 2. Prosedur Deployment
Gunakan Expo Application Services (EAS) untuk membangun paket staging.

### Android
```bash
npm run build:staging:android
```
*Atau:* `eas build --platform android --profile staging`

### iOS
```bash
npm run build:staging:ios
```
*Atau:* `eas build --platform ios --profile staging`

## 3. Verifikasi Pasca-Deployment
Setelah build selesai, lakukan langkah berikut:
1. Unduh APK/IPA dari dashboard Expo.
2. Instal di perangkat uji.
3. Login menggunakan akun tester staging.
4. Verifikasi koneksi API dengan membuka menu **Legal Search**.
5. Pastikan fitur **Collaborative Editor** dapat memuat dokumen.

## 4. Akses Tim Legal
Tim legal dapat mengakses build staging melalui:
- **Expo Go** (untuk testing cepat): Scan QR code dari dashboard Expo.
- **Install Langsung**: Link download build yang dihasilkan oleh EAS.

---
*Dibuat oleh Agent - 2026-01-18*
