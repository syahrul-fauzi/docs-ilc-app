## 1. Persona Pengguna

### 1.1 Persona A: Budi (Masyarakat Umum)
- **Latar Belakang**: Wiraswasta, tidak memiliki latar belakang hukum.
- **Tujuan**: Mendapatkan jawaban cepat atas masalah sehari-hari (sewa menyewa, hutang piutang).
- **Pain Points**: Bingung dengan istilah hukum "prokem", takut biaya pengacara mahal.
- **Kebutuhan**: Penjelasan dengan bahasa sederhana, ringkasan eksekutif, dan referensi pasal yang valid.

### 1.2 Persona B: Sarah (Advokat Junior)
- **Latar Belakang**: Lulusan hukum baru, bekerja di firma hukum.
- **Tujuan**: Melakukan riset hukum awal untuk kasus klien dengan cepat.
- **Pain Points**: Waktu riset manual di JDIH seringkali lama dan tidak terorganisir.
- **Kebutuhan**: Analisis mendalam, referensi UU/PP/Perpres yang lengkap, dan kemampuan memverifikasi sumber secara langsung.

---

## 2. Identifikasi Kebutuhan & Solusi (Metode UCD)

| Kebutuhan (User Needs) | Solusi Desain (UX Proposal) |
| :--- | :--- |
| **Kepastian & Kepercayaan** | Implementasi *Trust Badge* (Confidence Score) dan link langsung ke dokumen JDIH asli. |
| **Kemudahan Input** | *Unified Input Zone* yang mendukung Teks, Suara (dengan transkripsi real-time), dan Scan Dokumen. |
| **Transparansi AI** | *Real-time Thought Stream* untuk menunjukkan langkah-langkah logika AI saat memproses jawaban. |
| **Efisien Memahami Hasil** | *Executive Summary* di awal jawaban untuk memberikan poin penting tanpa harus membaca seluruh teks. |
| **Aksesibilitas Inklusif** | Ukuran font minimal 16px, target sentuh 44px, dan dukungan penuh untuk screen reader (VoiceOver/TalkBack). |

---

## 3. Analisis Alur Pengguna (User Flow)

1. **Entry Point**: Pengguna masuk ke Tab "Ask".
2. **Context Setting**: Memilih kategori hukum (Pidana/Perdata) via chips.
3. **Input Query**: Mengetik, berbicara, atau memindai dokumen.
4. **Processing**: AI menampilkan "Thought Stream" (menganalisis, mencari dasar hukum).
5. **Output**: Menampilkan ringkasan eksekutif diikuti oleh analisis detail dan referensi.
6. **Interaction Loop**: Pengguna dapat bertanya lebih lanjut atau membagikan hasil riset.

---

## 4. Evaluasi Pain Points & Perbaikan

- **Hambatan**: Pengguna sering merasa "terintimidasi" oleh layar kosong.
- **Perbaikan**: Tambahkan `AskQuickTips` dan `TrendingTopics` untuk memberikan inspirasi pertanyaan.
- **Hambatan**: Jawaban AI yang terlalu panjang sering tidak dibaca sampai selesai.
- **Perbaikan**: Gunakan struktur *Inverted Pyramid* (Ringkasan -> Detail -> Pendukung).

---
*Dokumen ini merupakan bagian dari siklus pengembangan ILC-APP berdasarkan data analisis per 18 Januari 2026.*
