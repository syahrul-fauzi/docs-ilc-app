# 🚀 Deployment Guide (Expo EAS)

## 🛠 Persiapan
1. Pastikan `app.json` memiliki `version` dan `buildNumber` yang benar.
2. Login ke EAS: `eas login`.

## 📦 Build Process
- **Staging**: `eas build --profile staging --platform all`
- **Production**: `eas build --profile production --platform all`

## 📤 Submission
- Kirim ke toko aplikasi: `eas submit --platform ios/android`