# Development Readiness Audit — ILC-APP

Analisis kesiapan lingkungan pengembangan dan rekomendasi toolchain.

## 1. Identifikasi Gaps
- **Dokumentasi Onboarding**: `QUICK_START.md` sudah ada namun perlu detail teknis tambahan terkait setup emulator dan debugging.
- **Environment Setup**: Perlu panduan eksplisit untuk pengelolaan `.env` dan rahasia (secrets).
- **Automation**: Belum ada pre-commit hooks (Husky) untuk memastikan lint dan test dijalankan otomatis.
- **Toolchain Standard**: Belum ada daftar ekstensi IDE yang direkomendasikan untuk tim.

## 2. Rekomendasi Toolchain
- **IDE**: VS Code.
- **Ekstensi VS Code**:
  - ESLint
  - Prettier
  - Tailwind CSS IntelliSense
  - Expo Tools
  - Jest Runner
- **Node.js**: Versi LTS (v18.x atau v20.x).
- **Package Manager**: npm (v9+).
- **Debugger**: React Native Debugger atau Expo DevTools.

## 3. Checklist Persiapan Environment (Setup Guide)
Daftar langkah untuk developer baru:
1. **Node & npm**: Pastikan Node.js LTS terinstal.
2. **Global Deps**: `npm install -g expo-cli eas-cli`.
3. **Repository**: `git clone [url]` dan `npm install`.
4. **Environment**: Buat file `.env` berdasarkan `.env.example`.
5. **Emulator/Device**:
   - Android: Install Android Studio & Setup Emulator.
   - iOS (macOS): Install Xcode & Simulator.
   - Physical: Install aplikasi "Expo Go" di smartphone.
6. **Verification**: Jalankan `npx expo start` dan pastikan aplikasi terbuka di salah satu platform.

## 4. Konfigurasi yang Diperlukan (Upcoming)
- Setup **Husky** & **lint-staged**.
- Konfigurasi **EAS Build** untuk integrasi CI/CD.
- Penambahan **Sentry** untuk error tracking di production.
