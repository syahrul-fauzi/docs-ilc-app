# ⚖️ Legal UAT Test Cases - ILC-APP

Dokumen ini berisi daftar skenario pengujian untuk tim legal guna memverifikasi keakuratan, kepatuhan, dan fungsionalitas aplikasi di lingkungan Staging.

## 1. AI Legal Engine (Ask AI)
| ID | Skenario | Langkah | Hasil yang Diharapkan | Status |
|----|----------|---------|-----------------------|--------|
| AI-01 | Akurasi Referensi Pasal | Tanyakan "Apa syarat sah perjanjian menurut KUH Perdata?" | AI menyebutkan Pasal 1320 KUH Perdata dengan 4 syarat yang benar. | |
| AI-02 | Deteksi Yurisdiksi | Tanyakan "Syarat pendirian startup di Singapura" | AI mendeteksi yurisdiksi SG dan memberikan referensi ACRA/Companies Act. | |
| AI-03 | Trust Signals | Periksa hasil pencarian hukum | Muncul badge "Verified Source" atau "Official Source" (.go.id). | |
| AI-04 | Disclaimer Hukum | Tanyakan kasus perceraian atau pidana | Muncul disclaimer bahwa jawaban bukan nasihat hukum formal. | |

## 2. Analisis Dokumen AI
| ID | Skenario | Langkah | Hasil yang Diharapkan | Status |
|----|----------|---------|-----------------------|--------|
| DOC-01 | Analisis Kontrak Sewa | Unggah/Tempel draf kontrak sewa menyewa | AI mengidentifikasi risiko (misal: tidak ada klausul force majeure). | |
| DOC-02 | Personalisasi Insight | Lakukan analisis draf berulang kali | AI memberikan saran berdasarkan gaya drafting sebelumnya (MemoryService). | |
| DOC-03 | Deteksi Klausul Hilang | Analisis draf NDA tanpa klausul kerahasiaan | AI menyarankan penambahan klausul kerahasiaan secara spesifik. | |
| DOC-04 | PII Masking | Masukkan draf dengan Nama & NIK asli | AI menyamarkan (masking) data sensitif sebelum diproses engine. | |

## 3. Collaborative Editor (Legal Tools)
| ID | Skenario | Langkah | Hasil yang Diharapkan | Status |
|----|----------|---------|-----------------------|--------|
| EDT-01 | Real-time Sync | Buka dokumen yang sama di dua perangkat | Perubahan di satu perangkat muncul instan di perangkat lain. | |
| EDT-02 | AI Smart Format | Gunakan fitur format otomatis | Penomoran pasal (Pasal 1, Pasal 2, dst) menjadi rapi dan konsisten. | |
| EDT-03 | Penjelasan Istilah | Klik istilah "Wanprestasi" di editor | Muncul tooltip/popover penjelasan istilah hukum tersebut. | |

## 4. Community Hub & Social
| ID | Skenario | Langkah | Hasil yang Diharapkan | Status |
|----|----------|---------|-----------------------|--------|
| COM-01 | Post Case Highlight | Buat postingan tentang ringkasan kasus | Postingan berhasil dibuat dan muncul di feed. | |
| COM-02 | AI Insight on Post | Lihat postingan di feed | Muncul "AI Insight" yang memberikan analisis singkat atas kasus tersebut. | |

## Mekanisme Pelaporan Temuan (Real-time Feedback)
Tim Legal kini dapat melaporkan temuan secara langsung dari dalam aplikasi menggunakan fitur **UAT Feedback**:

1. **Tombol UAT Feedback**: Klik ikon ⚠️ (Exclamation Bubble) yang tersedia di:
   - **Chat AI**: Di bawah setiap pesan balasan AI.
   - **Legal Editor**: Di bilah alat (toolbar) bagian atas.
2. **Pengisian Form**:
   - **Scenario ID**: Masukkan ID dari tabel di atas (misal: `AI-01`).
   - **Tipe**: Pilih antara `Bug` (error teknis), `Legal Inaccuracy` (salah hukum), atau `Improvement`.
   - **Severity**: Pilih tingkat keparahan (`Critical`, `Major`, `Minor`).
   - **Deskripsi**: Jelaskan temuan Anda, apa yang diharapkan, dan apa yang sebenarnya terjadi.
3. **Otomatisasi**: Sistem akan otomatis merekam konteks teknis (ID Task, Jalur Penalaran AI, dll) untuk membantu tim teknis melakukan perbaikan dengan cepat.

---
*Dikelola oleh Tim Lawyers Hub - Update Terakhir: 2026-01-18*
