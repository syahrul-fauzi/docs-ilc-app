# 🌍 Theming & Localization (ASEAN Ready)

## 🎨 Theming Strategy
- **Adaptive UI**: Mendukung Dark & Light mode menggunakan Ag-UI theme provider.
- **Brand Consistency**: Warna tema yang dapat disesuaikan per region jika diperlukan untuk kampanye lokal (e.g., warna asosiasi hukum lokal).

## 🌏 Localization Engine (ASEAN Expansion)
### 1. Multi-Language Support
- Menggunakan `i18next` sebagai engine lokalisasi.
- **Baseline**: Bahasa Indonesia (id) dan English (en).
- **Expansion Pipeline**: Penambahan Bahasa Malaysia (ms), Tagalog (tl), Thai (th), dan Vietnamese (vi) sesuai roadmap ekspansi regional.

### 2. Jurisdiction-Specific Localization
- Lokalisasi bukan hanya bahasa, tapi juga terminologi hukum spesifik negara (misal: "Advokat" di ID, "Barrister/Solicitor" di MY/SG).
- Format tanggal, mata uang (IDR, MYR, PHP, SGD), dan zona waktu otomatis menyesuaikan region pengguna.

### 3. Localization Workflow
- Pemisahan file lokalisasi per fitur untuk meminimalkan ukuran bundle.
- Integrasi dengan CMS untuk update konten *Daily Digest* dan *Community Feed* tanpa perlu update aplikasi (Over-the-Air updates via Expo).
