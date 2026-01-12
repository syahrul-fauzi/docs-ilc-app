# 🧭 Panduan Perbaikan Navigator Registration

Dokumen ini menjelaskan solusi untuk error "Couldn't register the navigator" yang terjadi akibat konflik versi `@react-navigation` dalam arsitektur monorepo.

## Deskripsi Masalah
Error: `Couldn't register the navigator. Have you wrapped your app with 'NavigationContainer'?`
Penyebab utama adalah adanya beberapa salinan paket `@react-navigation/native` dengan versi berbeda (misal: v6 dan v7) yang terinstal di `node_modules` root dan `node_modules` aplikasi.

## Langkah-langkah Solusi

### 1. Sinkronisasi Versi di `package.json`
Gunakan fitur `overrides` (NPM) atau `resolutions` (Yarn) untuk memaksa semua dependensi menggunakan versi yang sama.

```json
"overrides": {
  "@react-navigation/native": "^7.1.8",
  "@react-navigation/core": "^7.1.8",
  "@react-navigation/routers": "^7.1.8",
  "@react-navigation/stack": "^7.6.13",
  "@react-navigation/native-stack": "^7.3.16",
  "@react-navigation/bottom-tabs": "^7.4.0",
  "@react-navigation/elements": "^2.9.3"
}
```

### 2. Konfigurasi Metro Bundler
Paksa Metro untuk selalu meresolusi paket navigasi ke `node_modules` lokal aplikasi guna menghindari penggunaan paket yang ter-hoist ke root monorepo.

Edit `metro.config.js`:
```javascript
const navigationPackages = [
  "@react-navigation/native",
  "@react-navigation/core",
  "@react-navigation/routers",
  "@react-navigation/stack",
  "@react-navigation/native-stack",
  "@react-navigation/bottom-tabs",
  "@react-navigation/elements",
];

config.resolver.extraNodeModules = navigationPackages.reduce((acc, pkg) => {
  acc[pkg] = path.resolve(__dirname, "node_modules", pkg);
  return acc;
}, {});
```

### 3. "Un-hoisting" Manual (Jika Diperlukan)
Jika NPM tetap melakukan hoisting ke root, salin paket secara manual ke `node_modules` lokal:
```bash
cp -r ../../node_modules/@react-navigation/bottom-tabs node_modules/@react-navigation/
cp -r ../../node_modules/@react-navigation/native-stack node_modules/@react-navigation/
cp -r ../../node_modules/@react-navigation/stack node_modules/@react-navigation/
```

### 4. Pembersihan Cache
Selalu jalankan server dengan flag `--clear` setelah melakukan perubahan dependensi:
```bash
npx expo start --web --clear
```

## Verifikasi
1. Jalankan `npm list @react-navigation/native` dan pastikan tidak ada pesan "invalid" atau "deduped" ke versi yang salah.
2. Buka aplikasi di browser dan pastikan tidak ada overlay error "NavigationContainer".
