# UI/UX Improvement: AI Reasoning Process (v5 - True Trae Style)

Dokumen ini merinci evolusi final dari komponen **AI Reasoning Process** yang mengadopsi gaya "True Trae", ultra-lean, dan sepenuhnya inline dengan alur percakapan.

---

## 1. Filosofi Desain (True Trae)

Tujuan v5 adalah mencapai tingkat minimalisme tertinggi di mana elemen penalaran hampir tidak terasa sebagai UI tambahan, melainkan sebagai metadata halus dari sebuah respon.

- **Zero-Weight UI**: Menghapus border, margin kiri, dan aksen warna primer yang mencolok.
- **Micro-Typography**: Menggunakan font `11px` untuk header agar tidak bersaing dengan isi chat utama.
- **Faded Visuals**: Menggunakan opacity rendah (30-60%) untuk semua elemen dekoratif.

---

## 2. Spesifikasi UI Komponen

| Elemen | Spesifikasi v5 (True Trae) | Perubahan dari v4 |
| :--- | :--- | :--- |
| **Container** | `mb-2`, no border, no extra margin | Menghapus border-l dan margin kiri. |
| **Header Icon** | `brain.headlight.fill`, size `10px`, opacity `0.4` | Ukuran diperkecil, warna disamarkan. |
| **Status Text** | `11px`, `medium`, `muted-foreground/60` | Font lebih kecil, warna lebih pudar. |
| **Step Indicator** | `0.5x0.5` micro-dot, low opacity | Titik indikator hampir tidak terlihat. |
| **Step Content** | `12px`, `medium` prefix, `muted-foreground/70` | Menggunakan warna teks yang lebih tenang. |
| **Chevron** | size `8px`, opacity `0.3` | Sangat minimalis. |

---

## 3. Spesifikasi Interaksi & Animasi

### 3.1 Transisi Akordion
- **Duration**: `150ms` - Sangat cepat dan responsif.
- **Easing**: `Layout.springify().damping(28).stiffness(200)` - Efek pegas yang lebih kaku dan presisi.
- **Motion**: `FadeInDown` yang sangat singkat.

### 3.2 Staggered Step Entry
- **Delay**: `30ms` per langkah - Memberikan kesan data yang mengalir secara instan.
- **Type**: `timing` durasi `150ms`.
- **Motion**: Pure opacity fade, tanpa pergeseran posisi untuk menjaga stabilitas visual.

---

## 4. Panduan Implementasi Developer

Komponen utama: [ReasoningAccordion.tsx](file:///home/inbox/smart-ai/lawyers-hub/apps/ilc-app/src/shared/components/ui/ReasoningAccordion.tsx)

### Karakteristik Teknis:
1. **Low-Impact Rendering**: Sangat efisien karena menggunakan elemen minimal.
2. **Context-Aware Styling**: Menggunakan `muted-foreground` secara konsisten agar menyatu dengan background chat apa pun.

---
*Dikelola oleh Tim Super Agent - Update Terakhir: 2026-01-19 (v5 True Trae Style)*

## 5. Baru: Legal Reference Card (Citation Component)

Selain proses penalaran, sistem kini mendukung tampilan referensi hukum yang kaya akan konteks melalui komponen `LegalReferenceCard`.

### Karakteristik UI/UX:
- **Kategori Berbasis Warna**: Membedakan Perdata (Amber), Pidana (Red), Konstitusi (Blue), dll secara visual.
- **Interaktivitas**: Mendukung micro-interactions (scale on press), haptic feedback, dan integrasi Share API.
- **Desain Premium**: Menggunakan `border-l-4` untuk penekanan kategori dan background transparan yang elegan.

### Spesifikasi Teknis:
- **File**: [LegalReferenceCard.tsx](file:///home/inbox/smart-ai/lawyers-hub/apps/ilc-app/src/shared/components/ui/LegalReferenceCard.tsx)
- **Props**: `title`, `subtitle`, `content`, `category`, `onPress`.
- **Animasi**: Menggunakan `FadeInRight` dengan efek pegas (springify) untuk kemunculan yang dinamis.
