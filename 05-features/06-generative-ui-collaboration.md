# Generative UI & Collaborative Editing

Dokumen ini menjelaskan implementasi dan penggunaan sistem Generative UI serta fitur kolaborasi real-time di ILC-APP.

## 1. Generative UI

Generative UI memungkinkan AI untuk merespons tidak hanya dengan teks, tetapi dengan komponen UI dinamis yang disesuaikan dengan konteks hukum.

### Komponen yang Didukung
- **LegalSnippet**: Potongan teks hukum dengan tag dan sumber.
- **StatuteReference**: Referensi undang-undang dengan nomor pasal.
- **ActionGroup**: Kumpulan tombol aksi (misal: "Buat Draft", "Konsultasi").
- **ProceduralTimeline**: Visualisasi langkah-langkah prosedur hukum dengan fitur *expandable details*.
- **LegalChart**: Visualisasi data statistik hukum (bar, pie, line) dengan *interactive tooltips*.
- **DocumentPreview**: Preview draf dokumen dengan navigasi antar bagian.
- **AIRecommendation**: Saran strategis dari AI dengan label prioritas (High/Medium/Low).
- **ExportAction**: Tombol ekspor cepat ke format PDF/Docx.
- **LayoutStack/Grid**: Pengatur tata letak komponen.

### Aksesibilitas
Seluruh komponen Generative UI telah dioptimalkan untuk aksesibilitas:
- Penggunaan `accessibilityLabel` untuk pembaca layar (Screen Reader).
- Peran komponen yang jelas (`role="button"`, `role="summary"`, dll).
- Kontras warna yang memenuhi standar WCAG untuk keterbacaan tinggi.

### Integrasi
Komponen ini di-render melalui `GenerativeRenderer` yang menerima spesifikasi dalam format JSON dari `AgentOrchestrator`.

```typescript
// Contoh Spesifikasi
{
  type: 'procedural-timeline',
  steps: [
    { title: 'Pendaftaran', status: 'completed' },
    { title: 'Verifikasi', status: 'current' }
  ]
}
```

## 2. Kolaborasi Real-time (Yjs)

Fitur kolaborasi memungkinkan beberapa pengguna (pengacara dan klien) untuk menyusun dokumen hukum secara bersamaan.

### Fitur Utama
- **Real-time Sync**: Sinkronisasi perubahan teks secara instan menggunakan algoritma CRDT (Yjs).
- **Offline Support**: Penyimpanan lokal menggunakan IndexedDB sehingga pengeditan tetap bisa dilakukan tanpa koneksi.
- **Awareness**: Indikator pengguna yang sedang aktif di dalam dokumen.
- **Version History**: Kemampuan untuk menyimpan snapshot versi dan melakukan restore ke versi sebelumnya.
- **AI-Assisted Drafting**: Integrasi dengan AI untuk memberikan saran perbaikan terminologi hukum.

### Implementasi Teknis
- **Service**: `LegalEditorService.ts`
- **UI Component**: `CollaborativeEditor.tsx`
- **Provider**: WebRTC untuk komunikasi P2P (signaling server: yjs.dev).

## 3. Standar UI/UX (NativeWind v4)

Semua komponen UI dibangun menggunakan NativeWind v4 untuk memastikan:
- **Konsistensi**: Menggunakan sistem desain atomik (Ag-UI).
- **Responsivitas**: Layout yang adaptif untuk ponsel dan tablet.
- **Animasi**: Micro-animations menggunakan React Native Reanimated untuk feedback pengguna yang lebih baik.

---
*Dikelola oleh Tim Lawyers Hub - Terakhir Diperbarui: 2026-01-11*
