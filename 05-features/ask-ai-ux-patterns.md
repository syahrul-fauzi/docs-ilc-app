# Pola UX (UX Patterns) pada Fitur Ask AI

Dokumen ini menjelaskan pola-pola UX yang diterapkan pada fitur Ask AI di ILC-APP untuk meningkatkan pengalaman pengguna, transparansi, dan kepercayaan.

---

## 1. Context-Aware Input
**Lokasi**: `SearchInputCard.tsx`
- **Deskripsi**: Sistem memberikan saran otomatis (*Smart Suggestions*) dan kategori kontekstual (*Category Chips*) saat pengguna mulai berinteraksi.
- **Tujuan**: Mengurangi beban kognitif pengguna dalam merumuskan pertanyaan hukum yang kompleks.
- **Implementasi**: 
  - `filteredSuggestions`: Menampilkan 3 saran teratas berdasarkan input teks.
  - `CategoryChips`: Memungkinkan pengguna membatasi domain hukum (Pidana, Perdata, Bisnis) sejak awal.

## 2. Transparent Processing (Thought Stream)
**Lokasi**: `ThinkingAgent.tsx`
- **Deskripsi**: Menampilkan langkah-langkah internal AI secara real-time selama proses analisis.
- **Tujuan**: Membangun kepercayaan (*Trust*) dengan menunjukkan bahwa AI melakukan riset pada sumber yang valid, bukan sekadar "menebak".
- **Implementasi**: 
  - Prop `currentActivity` menerima update status dari `AgentOrchestrator` (misal: "Menganalisis Pasal 362 KUHP").

## 3. Inverted Pyramid Writing (Executive Summary)
**Lokasi**: `MessageBubble.tsx`
- **Deskripsi**: Menyajikan informasi paling penting (Ringkasan Eksekutif) di bagian paling atas, diikuti oleh detail hukum dan referensi pendukung.
- **Tujuan**: Memudahkan pengguna mendapatkan inti jawaban dengan cepat tanpa harus membaca narasi hukum yang panjang dan kaku.
- **Implementasi**: 
  - Komponen `ExecutiveSummary` mengekstrak atau menyusun poin-poin kunci di awal balon pesan.

## 4. Progressive Disclosure
**Lokasi**: `AskTuningModal.tsx`
- **Deskripsi**: Menyembunyikan opsi konfigurasi canggih di balik satu titik akses (tombol "Tuning") untuk menjaga kebersihan antarmuka utama.
- **Tujuan**: Mencegah *Information Overload* bagi pengguna baru, namun tetap memberikan kontrol penuh bagi pengguna mahir (*Power Users*).
- **Implementasi**: 
  - Modal yang berisi pengaturan Gaya Percakapan, Nada Bicara, dan Domain Spesifik.

## 5. Actionable Error Recovery
**Lokasi**: `AskFooter.tsx`
- **Deskripsi**: Menyediakan pesan kesalahan yang deskriptif dan manusiawi disertai dengan tombol tindakan pemulihan yang jelas.
- **Tujuan**: Mengurangi frustrasi pengguna saat terjadi kegagalan sistem atau koneksi.
- **Implementasi**: 
  - Tombol "Coba Lagi" (Retry) yang menonjol dengan label aksesibilitas yang lengkap.

---
*Dikelola oleh Tim Lawyers Hub - Update Terakhir: 2026-01-18*
