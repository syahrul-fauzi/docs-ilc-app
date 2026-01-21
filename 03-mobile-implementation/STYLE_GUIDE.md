# 🎨 Style Guide Komponen ILC-APP

Dokumen ini mendefinisikan standar visual, interaksi, dan penggunaan komponen UI dalam proyek **ILC-APP**.

## 1. Prinsip Desain
- **Modern & Bersih**: Menggunakan spacing yang lega, sudut membulat, dan bayangan halus.
- **Konsisten**: Mengikuti token desain yang didefinisikan di `global.css`.
- **Aksesibel**: Kontras warna tinggi, dukungan screen reader, dan target sentuh minimal 44x44px.
- **Agentic Feel**: Memberikan feedback instan melalui animasi dan haptic.

## 2. Token Desain Dasar
- **Radius**: 
  - `rounded-xl` (12px) untuk input dan tombol kecil.
  - `rounded-2xl` (16px) untuk card dan komponen menengah.
  - `rounded-3xl` (24px) untuk dialog dan bottom sheets.
- **Shadow**: 
  - `shadow-sm` untuk elemen halus.
  - `shadow-md` untuk card.
  - `shadow-xl` untuk modal dan toast.
- **Typography**:
  - `h1`: 32px, Bold
  - `h2`: 24px, Bold
  - `base`: 16px, Regular/SemiBold (Default mobile)
  - `small`: 14px, Medium

## 3. Komponen Inti

### Button (`button.tsx`)
Gunakan untuk aksi utama. Mendukung micro-interactions (scale) dan haptic feedback.
- **Primary**: `variant="default"` (Blue-33)
- **Secondary**: `variant="secondary"`
- **Outline**: Untuk aksi sekunder.
- **Destructive**: Untuk aksi berbahaya (Hapus, Keluar).

### Input (`input.tsx`)
- Gunakan `leftIcon` untuk memberikan konteks visual (misal: ikon email).
- Pastikan menyertakan `accessibilityLabel` dan `accessibilityHint`.
- Menangani state `error` secara otomatis dengan animasi `Moti`.

### Select (`select.tsx`)
- Pengganti picker native untuk kontrol visual yang lebih baik.
- Mendukung animasi dropdown dan state error.

### Dialog (`dialog.tsx`)
- Menggunakan animasi spring untuk entry yang halus.
- Backdrop otomatis menangani penutupan saat diketuk.

### Toast (`toast.tsx`)
- Digunakan untuk notifikasi sistem.
- Posisi otomatis menyesuaikan dengan `Safe Area` perangkat.
- Mendukung tipe: `success`, `error`, `warning`, `info`.

## 4. Standar Animasi (Moti)
Semua komponen interaktif harus menggunakan transisi yang halus:
- **Entry**: `from={{ opacity: 0, scale: 0.95 }}`
- **Animate**: `animate={{ opacity: 1, scale: 1 }}`
- **Transition**: Gunakan `type: 'spring'` untuk elemen UI utama dan `type: 'timing'` untuk elemen dekoratif.

## 5. Aksesibilitas (A11y)
- Selalu gunakan `accessibilityLabel` pada tombol tanpa teks.
- Gunakan `accessibilityRole` yang tepat (button, header, alert, dll).
- Pastikan target sentuh (Pressable) memiliki area yang cukup.

---
*Dikelola oleh Tim Lawyers Hub - Update Terakhir: 2026-01-19*
