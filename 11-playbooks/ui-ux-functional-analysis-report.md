# Laporan Analisis UI/UX & Fungsional ILC-APP

## 1. Analisis UI (User Interface)

### Temuan Utama
- **Konsistensi Visual**: Terdapat ketidakkonsistenan pada radius sudut (*border-radius*). Komponen `Button` dan `Input` menggunakan `rounded-xl` (12px-16px), sedangkan `Card` menggunakan `rounded-lg` (8px).
- **Tipografi**: Penggunaan font Inter sudah konsisten. Namun, pada layar kecil, `h1` (40px) mungkin terlalu dominan dan menyebabkan pemotongan teks (*text wrapping*) yang tidak elegan.
- **Palet Warna**: Kontras warna pada `muted-foreground` di mode gelap perlu diperiksa kembali untuk memenuhi standar aksesibilitas WCAG 2.1.
- **Responsivitas**: Layout menggunakan Flexbox dengan baik, namun beberapa komponen `Card` memiliki *padding* statis (`p-6`) yang mungkin terlalu besar untuk perangkat dengan layar sangat sempit (misal: iPhone SE).

### Rekomendasi
- Standarisasi *border-radius* ke `rounded-xl` untuk semua komponen utama guna menciptakan kesan modern dan bersahabat.
- Implementasikan *fluid typography* atau penyesuaian ukuran font berdasarkan lebar layar untuk varian `h1` dan `h2`.
- Gunakan *padding* responsif (misal: `native:p-4 md:p-6`).

---

## 2. Analisis UX (User Experience)

### Temuan Utama
- **Visibility of System Status**: Pesan status di `AskInputZone` sangat membantu. Namun, untuk proses multi-agen yang memakan waktu >5 detik, pengguna tidak mengetahui agen mana yang sedang bekerja.
- **User Control**: Deteksi konteks (Drafting/Research) berbasis kata kunci bisa salah sasaran. Pengguna tidak memiliki cara manual untuk mengoreksi konteks jika deteksi otomatis keliru.
- **Friction Points**: Transisi antara hasil pencarian hukum dan editor dokumen (Yjs) masih terasa terputus (*disconnected*).

### Rekomendasi
- Tambahkan **Progress Indicator** bertingkat di UI saat `AgentOrchestrator` sedang berjalan (misal: "Peneliti sedang mencari JDIH..." -> "Analis sedang meninjau pasal...").
- Tambahkan **Manual Context Switcher** (Toggle) di dekat input bar agar pengguna bisa memilih mode secara eksplisit.
- Integrasikan *Deep Link* atau *Floating Action Button* (FAB) untuk langsung membuka draf dokumen dari hasil analisis AI.

---

## 3. Analisis Fungsional

### Temuan Utama
- **Logika Bisnis**: Implementasi kebijakan (Pro Bono, ASEAN, Disclaimer) sangat kuat dan sesuai dengan regulasi.
- **Integrasi API**: `AgentOrchestrator` sudah terhubung dengan baik ke berbagai layanan (Billing, Memory, Regional).
- **Validasi Input**: Belum ada validasi tipe file atau batas karakter yang ketat pada input zona sebelum dikirim ke AI.

### Rekomendasi
- Tambahkan validasi *client-side* untuk input query (misal: minimal 10 karakter untuk hasil optimal).
- Implementasikan mekanisme *fallback* atau *retry* otomatis jika salah satu agen (misal: `ResearcherAgent`) mengalami kegagalan atau *timeout*.
- Tambahkan *rate-limiting* di sisi UI untuk mencegah pengiriman kueri bertubi-tubi yang bisa membebani biaya API.

---

## 4. Prioritas Perbaikan

| No | Fitur | Masalah | Urgensi | Dampak |
|---|---|---|---|---|
| 1 | UI Consistency | Border-radius tidak seragam | Medium | Low |
| 2 | UX Progress | Status agen tidak detail | High | Medium |
| 3 | Functional | Validasi input query | Medium | Medium |
| 4 | UX Control | Manual context toggle | High | High |
| 5 | UI Responsive | Padding Card di layar kecil | Low | Low |

---

## 5. Rencana Implementasi & Roadmap

### Fase 1: Quick Wins (Minggu 1)
- Penyeragaman `border-radius` ke `rounded-xl`.
- Penyesuaian *padding* responsif pada komponen `Card`.
- Penambahan validasi minimal karakter pada `AskInputZone`.

### Fase 2: UX Enhancement (Minggu 2)
- Implementasi **Step-by-step Progress Indicator** pada `MessageBubble` atau `AskInputZone`.
- Penambahan **Manual Context Toggle** untuk Research/Drafting/Analysis.

### Fase 3: Robustness (Minggu 3)
- Implementasi mekanisme *retry* pada `AgentOrchestrator`.
- Audit kontras warna dan aksesibilitas menyeluruh.

### Metrik Keberhasilan
- Penurunan *bounce rate* pada layar "Ask" sebesar 15%.
- Peningkatan akurasi deteksi konteks (melalui *feedback* pengguna) hingga 95%.
- Kecepatan persepsi pengguna (*perceived speed*) meningkat dengan adanya indikator progres yang detail.

### Rencana Pengujian Post-Implementasi
- **Unit Testing**: Memastikan validasi input dan logika *toggle* berfungsi.
- **Integration Testing**: Verifikasi status progres dari `AgentOrchestrator` terkirim ke UI.
- **UAT**: Sesi pengujian dengan 5 pengguna nyata untuk menilai kejelasan indikator progres baru.
