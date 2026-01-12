# Development Setup Checklist — ILC-APP

Ikuti panduan ini untuk menyiapkan lingkungan pengembangan mobile ILC-APP.

## 1. Prasyarat Tooling
- [ ] **Node.js**: Versi >= 18.x (Gunakan `nvm` jika perlu).
- [ ] **Package Manager**: `npm` (Bawaan Node.js).
- [ ] **Expo CLI**: `npx expo`.
- [ ] **Watchman**: (Hanya untuk macOS/Linux) Untuk performa file watching.
- [ ] **Java Development Kit (JDK)**: Versi 17 (Untuk build Android).
- [ ] **Android Studio**: Konfigurasi SDK, Build Tools, dan Emulator.
- [ ] **Xcode**: (Hanya untuk macOS) Untuk build iOS dan Simulator.

## 2. Persiapan Repositori
- [ ] Clone repositori: `git clone <repo-url>`.
- [ ] Masuk ke direktori: `cd lawyers-hub/apps/ilc-app`.
- [ ] Instal dependensi: `npm install`.
- [ ] **Monorepo Setup**:
  - Proyek ini menggunakan struktur monorepo. Jika Anda mengalami masalah dependensi (misal: duplicate React versions), pastikan `metro.config.js` telah dikonfigurasi dengan benar untuk memaksa resolusi modul ke `node_modules` lokal.
  - Gunakan `npm dedupe` jika diperlukan.

## 3. Konfigurasi Environment
- [ ] Buat file `.env` dari `.env.example`.
- [ ] Isi variabel `EXPO_PUBLIC_API_URL` dengan URL API server (staging/local).
- [ ] Isi API keys yang diperlukan (Copilotkit, etc.).

## 4. Verifikasi Setup
- [ ] Jalankan aplikasi di web: `npx expo start --web`.
- [ ] Jalankan aplikasi di emulator: `npx expo start -a` (Android) atau `npx expo start -i` (iOS).
- [ ] Jalankan test untuk memastikan semua OK: `npm test`.

## 5. VS Code Extensions (Rekomendasi)
- [ ] **ESLint**: Linter JavaScript/TypeScript.
- [ ] **Prettier**: Code formatter.
- [ ] **Tailwind CSS IntelliSense**: Untuk NativeWind/Tailwind.
- [ ] **Expo Tools**: Debugging dan integrasi Expo.

---
*Jika menemui masalah, silakan cek [Troubleshooting Guide](../11-playbooks/README.md).*
