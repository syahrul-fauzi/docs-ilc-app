# 🛠 Log Perbaikan Teknis ILC-APP

Dokumen ini mencatat analisis akar penyebab, solusi, dan verifikasi untuk masalah teknis yang ditemukan selama pengembangan.

---

## 1. Mismatch Tipe IconSymbol (SFSymbols7_0)

**Masalah**: Error tipe data saat menggunakan nama icon MaterialIcons pada komponen `IconSymbol` karena tipe data yang diharapkan adalah `SFSymbols7_0`.
**Akar Penyebab**: Komponen `IconSymbol.tsx` menggunakan mapping yang tidak secara eksplisit mendefinisikan tipe kunci dan nilai untuk platform Android/Web (MaterialIcons).
**Solusi**: 
- Menambahkan tipe `Record<string, ComponentProps<typeof MaterialIcons>["name"]>` pada `IconMapping`.
- Menggunakan `as const` pada definisi kategori di `index.tsx`.
**Verifikasi**: Error TypeScript hilang pada `index.tsx` dan `consult.tsx`.

## 2. TouchableOpacity Missing Import

**Masalah**: `ReferenceError: Can't find variable: TouchableOpacity` pada `consult.tsx`.
**Akar Penyebab**: Komponen `TouchableOpacity` digunakan dalam kode tetapi tidak diimpor dari `react-native`.
**Solusi**: Menambahkan `TouchableOpacity` ke daftar impor dari `react-native`.
**Verifikasi**: Screen Consult dapat dirender tanpa error runtime.

## 3. Properti onPress pada Komponen Card

**Masalah**: Properti `onPress` tidak didukung secara langsung oleh komponen `Card` dari library UI kustom.
**Akar Penyebab**: Komponen `Card` didefinisikan sebagai `View` yang tidak memiliki event handler `onPress`.
**Solusi**: Membungkus komponen `Card` dengan `TouchableOpacity` untuk menangani event klik.
**Verifikasi**: Interaksi klik pada kartu pengacara dan kategori berfungsi dengan benar.

## 4. Mismatch Tipe BillingBreakdown vs number

**Masalah**: Error tipe saat menetapkan hasil `billingService.getDynamicPrice` ke properti `price` pada objek `Lawyer`.
**Akar Penyebab**: Interface `Lawyer` mengharapkan `price: number`, sedangkan `getDynamicPrice` mengembalikan objek `BillingBreakdown`.
**Solusi**:
- Memperbarui interface `Lawyer` untuk mendukung `price: number | BillingBreakdown`.
- Menambahkan logika ekstraksi harga (`typeof lawyer.price === 'number' ? lawyer.price : lawyer.price.total`) saat melakukan formatting mata uang.
**Verifikasi**: Tipe data konsisten dan tampilan harga di UI akurat (termasuk pajak).

## 5. React 19 / react-test-renderer Compatibility

**Masalah**: `TypeError: Cannot read properties of undefined (reading 'ReactCurrentOwner')` saat menjalankan unit test.
**Akar Penyebab**: React 19 mengubah struktur internal (`__SECRET_INTERNALS...`) yang digunakan oleh `react-test-renderer` versi lama atau yang belum sepenuhnya kompatibel.
**Solusi**: (Dalam proses) Menambahkan patch di `jest.setup.js` untuk mengalias `__CLIENT_INTERNALS...` ke `__SECRET_INTERNALS...` dan memastikan `ReactCurrentOwner` terdefinisi.
**Catatan**: Masalah ini bersifat lingkungan (node_modules) dan disarankan untuk menunggu pembaruan resmi dari library terkait jika patch tidak sepenuhnya efektif.

---
*Terakhir Diperbarui: 2026-01-11*
