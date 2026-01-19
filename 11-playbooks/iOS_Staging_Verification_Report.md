# 📱 Laporan Verifikasi Staging iOS - ILC-APP

## 1. Informasi Build
- **EAS Build ID**: `[Isi EAS Build ID]`
- **Build Profile**: `staging`
- **Versi Aplikasi**: `0.1.0`
- **Tanggal Pengujian**: 2026-01-16

## 2. Perangkat Pengujian
| Model Perangkat | Versi iOS | Screen Size/Density | Status |
|-----------------|-----------|---------------------|--------|
| iPhone 15 Pro   | 17.x      | 6.1" / 3x           | 🟡 Pending |
| iPhone 13 Mini  | 16.x      | 5.4" / 3x           | 🟡 Pending |
| iPad Air (M1)   | 17.x      | 10.9" / 2x          | 🟡 Pending |
| iPhone SE (3rd) | 15.x      | 4.7" / 2x           | 🟡 Pending |

## 3. Checklist Verifikasi Menyeluruh

### 3.1 Integrasi NativeWind (Styling)
- [ ] Warna tema (Primary, Secondary, Background) sesuai desain Ag-UI.
- [ ] Tipografi (Heading, Body, Small) terbaca jelas di semua density.
- [ ] Komponen Shadcn-UI (Button, Card, Badge) ter-render dengan benar.
- [ ] Responsivitas layout pada orientasi Portrait.
- [ ] Dukungan Dark Mode / Light Mode (Automatic).

### 3.2 Performa & Stabilitas Reanimated
- [ ] Animasi transisi layar (Expo Router) berjalan mulus (60 FPS).
- [ ] Animasi interaksi pada `CommunityFeed` (FadeInDown) tidak menyebabkan drop frame.
- [ ] Gesture handling pada chat list berfungsi tanpa delay.
- [ ] Penggunaan memori stabil saat scrolling daftar panjang.

### 3.3 Kompatibilitas Ukuran Layar
- [ ] SafeAreaView menangani Notch, Dynamic Island, dan Home Indicator dengan benar.
- [ ] Tidak ada elemen UI yang terpotong di perangkat layar kecil (iPhone SE).
- [ ] Layout memanfaatkan ruang layar besar secara optimal di iPad.

### 3.4 Fungsi Spesifik Platform iOS
- [ ] **Secure Store**: Login session tersimpan aman di Keychain.
- [ ] **Haptics**: Feedback getaran terasa pada aksi-aksi penting (Like, Post).
- [ ] **Permissions**: Alert permission (Camera, Photo Library) muncul sesuai standar iOS.
- [ ] **Status Bar**: Warna dan visibilitas status bar sesuai dengan tema aplikasi.

## 4. Temuan Penting & Bug
| ID | Deskripsi Masalah | Perangkat | Prioritas | Status |
|----|-------------------|-----------|-----------|--------|
| - | - | - | - | - |

## 5. Kesimpulan & Rekomendasi
- **Status Verifikasi**: 🔴 Belum Dimulai
- **Rekomendasi**: Lakukan build staging dan jalankan checklist di atas sebelum melanjutkan ke build production.
