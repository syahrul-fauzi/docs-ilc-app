# 🚀 Linter & UX Optimization Playbook

Dokumen ini merangkum langkah-langkah stabilitas (Phase 1), peningkatan UX (Phase 2), dan optimasi performa (Phase 3) yang telah diimplementasikan pada ILC-APP.

---

## 1. Stabilitas (Phase 1: Linter Cleanup)

### Masalah yang Diselesaikan
- **React Hooks Compliance**: Memastikan semua hooks (`useState`, `useEffect`, `useCallback`) dipanggil sesuai urutan dan memiliki dependency array yang lengkap.
- **Unused Variables**: Pembersihan variabel dan parameter fungsi yang tidak digunakan di seluruh codebase layanan agen.
- **Consistent Formatting**: Penerapan standar linter yang konsisten menggunakan `expo lint`.

### Perubahan Utama
- Perbaikan pada `SplitViewReader.tsx` untuk mematuhi aturan hooks.
- Pembersihan parameter `userId`, `tenantId`, dan `sources` pada berbagai Agent (Analyst, Drafter, Researcher, Reviewer).
- Penambahan pre-commit hook menggunakan **Husky** dan **lint-staged** untuk mencegah regresi.

---

## 2. User Experience (Phase 2: Interactive Tutorial)

### Fitur Baru: Sentient Input Zone Tutorial
- **Interactive Walkthrough**: Panduan langkah-demi-langkah yang menjelaskan fitur deteksi konteks otomatis.
- **Highlighting Logic**: Area spesifik pada UI akan di-highlight (glowing/scaled) sesuai dengan langkah tutorial yang sedang aktif.
- **Context Awareness**: Tutorial menjelaskan bagaimana AI mendeteksi apakah pengguna sedang melakukan Research, Drafting, atau Analysis.
- **Persistence**: Status tutorial disimpan menggunakan `expo-secure-store` sehingga pengguna hanya melihatnya sekali.

---

## 3. Performa (Phase 3: Animation & Fallback)

### Strategi Optimasi
Untuk mencapai target 60fps yang konsisten, terutama pada perangkat entry-level, kami menerapkan sistem deteksi performa otomatis.

#### Performance Detection (`performanceService.ts`)
Sistem secara otomatis mengaktifkan **Low Performance Mode** jika:
- RAM Perangkat < 3GB.
- Versi Android < 10.
- Model perangkat terdeteksi sebagai "Go Edition".

#### Mekanisme Fallback
1. **Animation Scaling**: Durasi animasi dipotong 50% (lebih cepat/instan) pada perangkat low-end untuk mengurangi beban frame rendering.
2. **Visual Simplification**: 
   - Shadow berat (`shadow-2xl`) diganti menjadi `shadow-sm`.
   - Efek glow kompleks dinonaktifkan.
3. **Memoization**: Penggunaan `useMemo` dan `useCallback` secara agresif pada komponen yang sering re-render.

### Best Practices untuk Tim
- Selalu gunakan `performanceService.getAnimationDuration()` untuk mendefinisikan durasi animasi.
- Hindari penggunaan shadow berat pada komponen yang sering bergerak di perangkat low-end.
- Gunakan `canRenderHeavyGlows()` untuk menyembunyikan efek visual yang mahal secara komputasi.

---
*Terakhir Diperbarui: 2026-01-19*
