# 📄 F04: Document Automation & Collaborative Editor

## 📝 Deskripsi
Fitur untuk membantu pengguna dan pengacara menyusun dokumen hukum secara kolaboratif dengan bantuan AI. Fitur ini menggabungkan editor teks real-time dengan basis data template hukum yang cerdas.

## 🚀 Fitur Utama

### 1. Collaborative Legal Editor (Yjs Powered)
Editor teks yang mendukung kolaborasi multi-pengguna secara real-time.
- **Conflict-Free**: Menggunakan algoritma CRDT (Conflict-free Replicated Data Types) via [Yjs](https://yjs.dev/).
- **Real-time Sync**: Sinkronisasi instan antar perangkat menggunakan **WebRTC Provider**.
- **Awareness**: Menampilkan kursor dan identitas pengguna lain yang sedang mengedit secara aktif.
- **Offline Support**: Penyimpanan lokal otomatis menggunakan **IndexedDB Persistence**, memungkinkan pengeditan tanpa koneksi internet yang akan disinkronkan saat kembali online.

### 2. AI Legal Assistant (In-Editor)
Integrasi AI langsung di dalam editor untuk meningkatkan kualitas dokumen:
- **Smart Suggestions**: AI memberikan saran perbaikan klausul berdasarkan konteks dokumen (misalnya: menyarankan penambahan pasal *Force Majeure* atau penyelesaian sengketa).
- **Compliance Check**: Memastikan terminologi yang digunakan sesuai dengan regulasi terbaru (e.g., rujukan ke UU Cipta Kerja).
- **Tone Adjustment**: Mengubah gaya bahasa dokumen menjadi lebih formal atau sesuai dengan standar hukum Indonesia.

### 3. Automated Templates
Library template dokumen hukum yang siap pakai:
- Surat Perjanjian Kerjasama (MoU).
- Kontrak Kerja (PKWT/PKWTT).
- Dokumen Pendirian Usaha.
- Surat Kuasa.

## 🔄 Workflow & Implementation

### 1. Editor Lifecycle
1. **Initialization**: Saat membuka dokumen, `LegalEditorService` diinisialisasi dengan `roomName` unik.
2. **Persistence**: Mencoba memuat data dari IndexedDB untuk akses offline cepat.
3. **Collaboration**: Menghubungkan ke WebRTC signaling server untuk sinkronisasi dengan pengguna lain.
4. **Editing**: Pengguna melakukan perubahan yang secara otomatis disinkronkan ke semua peer.

### 2. AI Interaction
- Pengguna dapat memicu fungsi `suggestImprovements()` untuk mendapatkan daftar saran perbaikan dari AI.
- AI menganalisis teks dokumen dan memberikan feedback yang relevan secara hukum.

## ✅ Acceptance Criteria
- [ ] Kolaborasi real-time berjalan lancar antara minimal 2 perangkat.
- [ ] Dokumen tetap tersimpan secara lokal jika koneksi internet terputus.
- [ ] AI memberikan saran yang relevan sesuai dengan kategori hukum dokumen.
- [ ] Riwayat perubahan (Undo/Redo) berfungsi dengan benar di seluruh sesi kolaborasi.
