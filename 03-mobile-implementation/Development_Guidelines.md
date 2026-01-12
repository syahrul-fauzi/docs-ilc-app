# 🛠 Development Guidelines - ILC-APP

Panduan ini berisi standar koding, arsitektur, dan alur kerja untuk pengembangan aplikasi mobile ILC-APP menggunakan Expo.

---

## 1. Arsitektur Hybrid Modular

Kami menggunakan kombinasi **Feature-Sliced Design (FSD)** dan **Domain-Driven Design (DDD)** untuk skalabilitas maksimal.

### Aturan Utama:
- **Isolation**: Fitur tidak boleh mengimpor langsung dari fitur lain. Gunakan `shared` layer atau `public API` (index.ts).
- **Unidirectional Data Flow**: Data mengalir satu arah. UI -> Action -> Service -> State -> UI.
- **Strict Typing**: Gunakan interface yang kuat. Hindari `any`.

---

## 2. Standar Koding (Style Guide)

### 2.1 React & Expo
- Gunakan **Functional Components** dengan Hooks.
- Gunakan **Expo Router** untuk navigasi berbasis file.
- Hindari logic berat di dalam file `render`. Pindahkan ke custom hooks.

### 2.2 Styling (NativeWind)
- Gunakan variabel tema dari `constants/Colors.ts`.
- Contoh: `className="text-primary-500 font-bold"`.
- Gunakan `platform-specific` styling hanya jika diperlukan (`ios:`, `android:`).

### 2.3 State Management
- **Global State**: Recoil (untuk data lintas fitur).
- **Feature State**: React Context (untuk data di dalam satu fitur).
- **Local State**: `useState` / `useReducer`.

---

## 3. Alur Pengembangan Fitur Baru

1. **Planning**: Buat spesifikasi fitur menggunakan `docs/templates/Feature_Spec_Template.md`.
2. **Setup**: Buat folder fitur di `app/` atau `features/` (jika menggunakan struktur FSD penuh).
3. **UI/UX**: Implementasikan komponen UI menggunakan NativeWind.
4. **Service**: Hubungkan ke API menggunakan `lib/api/` client.
5. **Testing**: Buat unit test di folder `__tests__` yang relevan.
6. **Review**: Ajukan Pull Request (PR) dan pastikan CI lulus.

---

## 4. Troubleshooting & Best Practices

- **Performance**: Gunakan `FlashList` untuk daftar panjang. Pastikan `keyExtractor` unik.
- **Images**: Gunakan `expo-image` untuk caching dan performa.
- **Security**: Simpan token di `expo-secure-store`. Jangan commit `.env`.
- **Clean Up**: Selalu jalankan `npm run clean` jika terjadi masalah aneh dengan cache Expo.

---

## 5. Deployment

- Gunakan **EAS Build** untuk build biner.
- Gunakan **EAS Update** untuk perbaikan bug cepat tanpa update toko aplikasi.

---
*Last Updated: 2026-01-11*
