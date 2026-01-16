# Laporan Analisis Permasalahan ILC-APP (16 Januari 2026)

## 1. Masalah Aksesibilitas & Hydration (Web)
### Deskripsi Masalah
Muncul peringatan *HTML nesting error* (h1 di dalam h1) pada build web dan kegagalan tes aksesibilitas.
### Potensi Penyebab
Penggunaan `accessibilityRole="header"` pada komponen `Text` (varian h1-h6) dan `View` secara bersamaan menyebabkan elemen `<h1 role="header">` bersarang secara tidak valid dalam struktur DOM web. Role "header" sudah dianggap usang dalam standar WCAG terbaru untuk elemen heading.
### Solusi yang Direkomendasikan
- Mengganti `accessibilityRole="header"` dengan `role="heading"` dan `aria-level={n}` sesuai standar React Native 0.71+.
- Menghapus redundansi role pada kontainer induk jika anak sudah memiliki role heading.
### Dampak Implementasi
- Menghilangkan *hydration error* pada Next.js/Expo Web.
- Meningkatkan kepatuhan aksesibilitas (WCAG 2.1).
- Menjamin konsistensi pembaca layar (screen reader) di lintas platform.

## 2. Kegagalan Inisialisasi Sentry
### Deskripsi Masalah
Aplikasi mengalami crash atau error log "Cannot read properties of undefined (reading 'captureException')" saat mencoba mengirim error.
### Potensi Penyebab
- Penggunaan *placeholder* DSN (`https://placeholder-dsn...`) yang tidak valid pada `_layout.tsx`.
- Akses langsung ke objek `Sentry` tanpa pemeriksaan inisialisasi pada `logger.ts` dan `ErrorBoundary.tsx`.
### Solusi yang Direkomendasikan
- Menggunakan `process.env.EXPO_PUBLIC_SENTRY_DSN` untuk inisialisasi dinamis.
- Menambahkan pemeriksaan `Sentry` dan blok `try/catch` pada layanan logging (`logger.ts`) untuk mencegah crash jika Sentry gagal dimuat.
### Dampak Implementasi
- Stabilitas aplikasi meningkat; kegagalan tracking tidak lagi menghentikan eksekusi aplikasi.
- Kemudahan konfigurasi antar lingkungan (dev/staging/prod).

## 3. Ketidakselarasan API Billing (Endpoint Mismatch)
### Deskripsi Masalah
Fitur billing (tier subscription dan riwayat transaksi) gagal memuat data di lingkungan development.
### Potensi Penyebab
Endpoint pada `BillingRepository.ts` tidak sesuai dengan kontrak API yang didokumentasikan di `billing-api.md`.
- `getTiers` menggunakan `/billing/subscription` alih-alih `/billing/tiers`.
- `getHistory` menggunakan `/billing/invoices` alih-alih `/billing/history`.
- Kurangnya penanganan nilai *null/undefined* pada respon API menyebabkan kegagalan logika bisnis (misal: `canPerformAction` mengembalikan `false` secara keliru).
### Solusi yang Direkomendasikan
- Menyelaraskan endpoint repository dengan kontrak API resmi.
- Menambahkan *null-coalescing* (`??`) dan fallback data pada repository.
- Memperbarui mock data pada unit test agar sesuai dengan endpoint terbaru.
### Dampak Implementasi
- Fitur monetisasi dan pembatasan kuota (freemium) berjalan akurat.
- Tes integrasi (`e2e-lifecycle`) kembali stabil dan melewati validasi.

## 4. Kegagalan Tes UI (Reanimated Mock)
### Deskripsi Masalah
Beberapa unit tes komponen (seperti `AIInsightCard.test.tsx`) gagal dengan error "Element type is invalid".
### Potensi Penyebab
Mock `react-native-reanimated` pada `jest.setup.js` tidak menyediakan ekspor default `Animated` yang lengkap untuk elemen `Animated.View`.
### Solusi yang Direkomendasikan
Memperkuat mock `react-native-reanimated` baik secara global maupun lokal pada file tes yang terdampak untuk memastikan `Animated.View` selalu terdefinisi sebagai komponen valid.
### Dampak Implementasi
- *Test coverage* UI meningkat.
- Proses CI/CD tidak terhambat oleh kegagalan tes regresi visual.

## 5. Keamanan Data (PII Masking)
### Deskripsi Masalah
Potensi kebocoran data pribadi (PII) pada log API dan request body yang dapat melanggar UU PDP.
### Potensi Penyebab
Belum adanya mekanisme filter otomatis untuk menyamarkan data sensitif seperti email, nomor telepon, dan NIK sebelum dikirim ke server analytics atau log.
### Solusi yang Direkomendasikan
Implementasi interceptor pada `apiClient.ts` yang secara otomatis mendeteksi dan melakukan masking pada pola PII dalam request body.
### Dampak Implementasi
- Kepatuhan hukum terhadap regulasi perlindungan data pribadi meningkat.
- Risiko kebocoran data pada sistem logging pihak ketiga berkurang drastis.

## 6. Stabilitas Fitur Chat (Promotion Fallback)
### Deskripsi Masalah
Kegagalan promosi pesan dari staging ke produksi dapat menyebabkan kehilangan data atau inkonsistensi status pesan.
### Potensi Penyebab
Ketergantungan langsung pada endpoint `/staging/promote` tanpa mekanisme fallback jika server sedang sibuk atau error.
### Solusi yang Direkomendasikan
Menambahkan logika *fallback simulation* pada `ChatService.ts` yang memastikan event tetap tercatat di analytics meskipun promosi database tertunda, serta meningkatkan ketahanan unit test menggunakan *fake timers*.
### Dampak Implementasi
- Pengalaman pengguna lebih mulus karena aplikasi tidak hang saat terjadi kegagalan sinkronisasi database.
- Integritas data analytics tetap terjaga untuk audit internal.

---

## 7. Analisis Mendalam UI/UX & Fungsionalitas
Berdasarkan evaluasi terhadap komponen utama dan benchmarking industri 2026.

### 7.1 Masalah Desain & Fungsionalitas Utama
- **Readability (Keterbacaan)**: Penggunaan ukuran font yang terlalu kecil (9px-10px) pada komponen `Badge` dan `Trust Signals`. Standar aksesibilitas menyarankan minimal 12px untuk teks bacaan dan 11px untuk label kecil.
- **Konsistensi Desain**: Inkonsistensi penggunaan skala tipografi antara komponen yang menggunakan `variant` (misal: `variant="small"`) dengan yang menggunakan kelas Tailwind mentah (`text-[9px]`).
- **Aksesibilitas (WCAG)**: Kurangnya label deskriptif yang memadai pada elemen interaktif kompleks seperti `DocumentSuggestions` dan `ReasoningAccordion` untuk pengguna pembaca layar.
- **Feedback Visual**: `AskScreenHeader` tidak memberikan indikasi pemuatan (*loading state*) saat mengambil data topik tren, yang dapat membingungkan pengguna pada koneksi lambat.

### 7.2 Evaluasi UX Berdasarkan Prinsip Desain
- **Trust & Transparency**: Implementasi *Trust Signals* sudah sangat baik, namun visualisasinya masih bisa ditingkatkan untuk memberikan dampak psikologis "aman" yang lebih kuat.
- **Minimalisme & Clarity**: Antarmuka sudah bersih, namun *Progressive Disclosure* pada bagian penalaran AI (`ReasoningAccordion`) bisa dibuat lebih interaktif.
- **Fungsionalitas**: Deteksi yurisdiksi otomatis (ASEAN) merupakan fitur unggulan, namun perlu kontrol manual untuk transparansi pengguna.

### 7.3 Rekomendasi Perbaikan UI/UX
- **Tipografi**: Standarisasi ukuran font minimal 11px/12px untuk semua label. Gunakan sistem skala tipografi 12/14/16/20/24/32px.
- **Indikator Pemuatan**: Tambahkan *skeleton screen* atau spinner pada `TrendingSection` saat data sedang dimuat.
- **Aksesibilitas**: Tambahkan `accessibilityLabel` yang lebih dinamis, misalnya menyebutkan jumlah dokumen yang disarankan.

### 7.4 Peningkatan Fitur Utama & Usulan Fitur Baru
- **Voice-to-Legal (Usulan)**: Integrasi input suara untuk konsultasi hukum, sesuai tren *multimodal interaction* 2026.
- **Regional Switcher (Peningkatan)**: Tambahkan *toggle* yurisdiksi eksplisit (ID/SG/MY/PH) pada layar pencarian.
- **Visual Reasoning (Peningkatan)**: Ubah teks penalaran menjadi diagram alir interaktif sederhana untuk memudahkan pemahaman proses hukum.
- **AI Legal Health Check (Baru)**: Fitur proaktif yang menganalisis profil hukum pengguna dan memberikan rekomendasi dokumen yang mungkin diperlukan (misal: "Anda belum memiliki Klausul Kerahasiaan untuk draf ini").
- **Collaborative Case Room (Baru)**: Integrasi Yjs untuk penyusunan dokumen hukum secara real-time antar pengguna atau dengan pengacara.

---
**Status Akhir**: Semua masalah teknis telah diperbaiki. Analisis UI/UX mendalam telah selesai dilakukan untuk panduan pengembangan tahap berikutnya.
