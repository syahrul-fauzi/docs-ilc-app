# Analisis Heatmap & Eye-Tracking: Tab "Ask" (Simulasi)

Dokumen ini menyajikan analisis teoritis mengenai pola interaksi pengguna (Heatmap) dan fokus visual (Eye-Tracking) pada tab "Ask" aplikasi ILC. Analisis ini didasarkan pada prinsip-prinsip psikologi kognitif dan desain antarmuka yang telah diterapkan.

---

## 1. Analisis Eye-Tracking (Pola Visual)

Berdasarkan struktur visual tab "Ask", fokus mata pengguna diperkirakan mengikuti pola **"F-Pattern"** yang dimodifikasi untuk aplikasi mobile (Z-Pattern terfokus).

### 1.1 Titik Fokus Utama (Gaze Points)
1.  **Welcome Hero (Header Area)**: 
    - Pengguna akan melihat pesan sambutan dan badge kepercayaan ("Verified Legal Sources").
    - **Tujuan**: Membangun kredibilitas instan.
2.  **Input Zone (Search Bar)**:
    - Mata akan tertuju pada area input besar di tengah layar.
    - **Anotasi**: Penggunaan bayangan (shadow) dan border yang kontras saat fokus memperkuat daya tarik visual.
3.  **Action Buttons (Scan/Voice)**:
    - Ikon kamera dan mikrofon yang berwarna (Primary & Secondary) menarik perhatian setelah area teks.
4.  **Quick Tips (Onboarding)**:
    - Elemen animasi di bawah input bar menangkap perhatian mata yang bergerak ke bawah (Scanning).

### 1.2 Heatmap Fokus Visual
- **Zona Merah (Intensitas Tinggi)**: Area teks input dan tombol "Tanya AI".
- **Zona Kuning (Intensitas Menengah)**: Chips "Case Type" dan "Quick Tips".
- **Zona Hijau (Intensitas Rendah)**: Disclaimer di footer dan navigasi riwayat di pojok atas.

---

## 2. Analisis Heatmap (Pola Interaksi)

Heatmap simulasi ini memetakan area mana yang paling sering disentuh (Click/Tap Heatmap) dan area mana yang paling sering dilewati (Scroll Heatmap).

### 2.1 Click Heatmap (Peta Klik)
- **Hotspot 1: Area Input Teks**: Lokasi paling aktif karena merupakan pintu masuk utama interaksi.
- **Hotspot 2: Tombol "Tanya AI"**: CTA utama yang memiliki ukuran target sentuh besar (min 44px).
- **Hotspot 3: Chips Filter "Case Type"**: Pengguna cenderung mengeksplorasi kategori (misal: "Pidana") sebelum mengetik pertanyaan lengkap.
- **Hotspot 4: Tombol Suara (Mic)**: Diprediksi populer bagi pengguna yang ingin berkonsultasi secara naratif tanpa mengetik panjang.

### 2.2 Scroll Heatmap (Kedalaman Gulir)
- **80% Pengguna**: Tetap berada di "Above the Fold" (area yang terlihat tanpa scroll), berinteraksi dengan input bar.
- **50% Pengguna**: Melakukan scroll ke bawah untuk melihat "Trending Questions" dan "Quick Tips".
- **20% Pengguna**: Mencapai bagian disclaimer paling bawah.

---

## 3. Optimasi Berdasarkan Analisis

Berdasarkan simulasi di atas, beberapa optimasi telah diimplementasikan:

| Masalah Temuan | Optimasi UX yang Diterapkan |
| :--- | :--- |
| **Cognitive Load Tinggi**: Pengguna bingung harus mengetik apa. | **Solusi**: Penambahan `AskQuickTips.tsx` dan `TrendingSection.tsx` untuk memicu ide. |
| **Eye Fatigue**: Area input terlalu polos. | **Solusi**: Penambahan visual feedback (Animated border & Elevation) saat input difokuskan. |
| **Low Interaction on Footer**: Disclaimer jarang dibaca. | **Solusi**: Menggunakan pola *Progressive Disclosure* (Accordion) agar disclaimer tidak memakan ruang namun tetap mudah diakses. |
| **Missed Features**: Fitur scan kurang terlihat. | **Solusi**: Memposisikan ikon Scan dan Voice berdampingan di dalam area input dengan warna aksen yang berbeda. |

---

## 4. Kesimpulan
Tab "Ask" dirancang untuk meminimalkan hambatan kognitif dengan menempatkan elemen interaksi paling kritis di pusat perhatian visual pengguna, didukung oleh bantuan kontekstual di sekitarnya.

*Terakhir diperbarui: 2026-01-18*
