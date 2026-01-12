# 🛠 Troubleshooting: Test Await Hangs in ConsultScreen

## Deskripsi Masalah
Terdapat laporan mengenai pengujian `ConsultScreen` yang mengalami "hang" (berhenti merespon) saat menggunakan `await` pada fungsi-fungsi layanan yang di-mock. Masalah ini menyebabkan timeout pada pengujian integrasi.

## Akar Masalah (Root Cause)
Setelah investigasi mendalam, beberapa faktor yang berkontribusi terhadap masalah ini adalah:
1. **Mocking Core Components**: Komponen inti React Native (seperti `View`, `Text`, `TouchableOpacity`) tidak di-mock secara eksplisit atau tidak konsisten, menyebabkan ketidakstabilan saat `react-test-renderer` mencoba merender pohon komponen yang kompleks dengan NativeWind.
2. **Async Assertion Timing**: Penggunaan `await findByText` atau `await waitFor` tanpa timeout yang cukup atau tanpa memastikan state loading telah selesai.
3. **Mock Return Values**: Penggunaan `mockReturnValue` yang mengembalikan nilai sinkron pada fungsi yang seharusnya mengembalikan Promise (`async`), terkadang menyebabkan isu pada microtask queue di lingkungan pengujian tertentu.
4. **Environment Consistency**: Perbedaan antara `npx jest` dan lingkungan CI dalam menangani transpilasi `async/await`.

## Solusi yang Diimplementasikan
1. **Eksplisit Mocking React Native**: Menambahkan mock eksplisit untuk semua komponen inti React Native di awal file test untuk memastikan definisi yang stabil.
2. **Standarisasi Mock Service**: Menggunakan `mockResolvedValue` daripada `mockReturnValue` untuk fungsi layanan asinkron guna mensimulasikan perilaku dunia nyata secara lebih akurat.
3. **Peningkatan Assertion**: Menggunakan `waitFor` dengan timeout yang memadai (default 1000ms, ditingkatkan jika perlu) untuk menunggu perubahan state asinkron.
4. **Validasi Loading State**: Menambahkan test case khusus untuk memverifikasi bahwa loading spinner muncul dan hilang dengan benar, bahkan saat terjadi error (menggunakan blok `finally`).
5. **Aksesibilitas sebagai Selector**: Menggunakan `findByLabelText` sebagai metode utama untuk menemukan elemen interaktif, yang lebih stabil dan sekaligus memvalidasi kepatuhan aksesibilitas.

## Test Case yang Ditambahkan
- **Error Handling**: Memastikan UI tetap responsif dan berhenti memuat meskipun terjadi kegagalan pada API.
- **Booking Flow**: Memastikan interaksi tombol memicu alert konfirmasi dengan benar setelah melewati alur asinkron (analytics).

## Rekomendasi Selanjutnya
- Selalu gunakan `waitFor` saat menguji komponen yang memiliki `useEffect` dengan panggilan API.
- Pastikan semua komponen interaktif memiliki `accessibilityLabel` yang unik untuk memudahkan pengujian dan mendukung pengguna dengan kebutuhan khusus.
- Gunakan `jest.spyOn(Alert, 'alert')` untuk memverifikasi interaksi dialog sistem.
