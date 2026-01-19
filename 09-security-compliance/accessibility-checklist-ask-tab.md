# Accessibility Checklist: Tab "Ask" (WCAG 2.1 Level AA)

## 1. Pendahuluan
Checklist ini digunakan untuk memastikan fitur "Ask AI" mematuhi standar aksesibilitas internasional WCAG 2.1 Level AA, guna menjamin inklusivitas bagi seluruh pengguna, termasuk penyandang disabilitas.

## 2. Prinsip: Perceivable (Dapat Dilihat)

- [x] **1.1.1 Non-text Content**: Semua ikon (`IconSymbol`) memiliki `accessibilityLabel` yang deskriptif.
- [x] **1.4.3 Contrast (Minimum)**: Rasio kontras teks terhadap latar belakang minimal 4.5:1.
  - *Status*: Placeholder input ditingkatkan ke opasitas 0.8 (Fixed).
- [x] **1.4.4 Resize Text**: Teks dapat diperbesar hingga 200% tanpa kehilangan konten atau fungsionalitas.
  - *Status*: Menggunakan unit `text-[16px]` yang adaptif terhadap system font scaling.
- [x] **1.4.12 Text Spacing**: Jarak antar baris (leading) minimal 1.5x ukuran font untuk keterbacaan optimal.

## 3. Prinsip: Operable (Dapat Dioperasikan)

- [x] **2.1.1 Keyboard**: Semua elemen interaktif dapat diakses melalui navigasi keyboard/switch.
- [x] **2.4.7 Focus Visible**: Indikator fokus yang jelas saat bernavigasi menggunakan alat bantu.
- [x] **2.5.3 Label in Name**: Label teks pada tombol (misal: "Tanya AI") sesuai dengan nama aksesibilitasnya.
- [x] **2.5.5 Target Size**: Ukuran target sentuh minimal 44x44 dp.
  - *Status*: Filter chips, tombol kirim, dan tombol modal ditingkatkan ke min-height 44px (Fixed).

## 4. Prinsip: Understandable (Dapat Dipahami)

- [x] **3.2.4 Consistent Identification**: Ikon dan label untuk fungsi yang sama konsisten di seluruh aplikasi.
- [x] **3.3.1 Error Identification**: Pesan kesalahan terdeteksi secara otomatis dan dijelaskan dalam teks.
  - *Status*: `AskFooter` menampilkan pesan error yang jelas dengan tombol Retry (Fixed).
- [x] **3.3.2 Labels or Instructions**: Input field memiliki label yang tetap terlihat (tidak hilang saat mengetik).
  - *Status*: Form di `UatFeedbackModal` menggunakan label teks permanen (Fixed).

## 5. Prinsip: Robust (Tangguh)

- [x] **4.1.2 Name, Role, Value**: Komponen custom menggunakan role aksesibilitas yang tepat (misal: `accessibilityRole="button"`).
- [x] **4.1.3 Status Messages**: Pesan status (seperti "Thinking...") diumumkan oleh pembaca layar tanpa mengubah fokus.

## 6. Audit Komponen Spesifik (Status Jan 2026)

| Komponen | Isu Sebelumnya | Status | Perbaikan |
| :--- | :--- | :--- | :--- |
| `SearchInputCard` | Kontras placeholder rendah | ✅ Fixed | Opasitas ditingkatkan ke 0.8 |
| `MessageBubble` | Font trust badge 9px | ✅ Fixed | Ukuran ditingkatkan ke 11px |
| `WelcomeHero` | Font trust badge 10px | ✅ Fixed | Ukuran ditingkatkan ke 12px |
| `VoiceInput` | Tombol rekam kecil | ✅ Fixed | Ukuran ditingkatkan ke 80px |
| `AskTuningModal` | Opsi terlalu rapat | ✅ Fixed | Padding & target sentuh 48px |
| `AskFooter` | Pesan error samar | ✅ Fixed | Teks merah kontras dengan tombol Retry |

---
*Dikelola oleh Tim Accessibility ILC - Update Terakhir: 18 Januari 2026*
