# 🔤 Font Setup & Configuration Guide

## 📂 Struktur Direktori Font
Aset font disimpan di direktori root aplikasi untuk memastikan aksesibilitas dari berbagai modul.

```
apps/ilc-app/
├── assets/
│   └── fonts/
│       └── SpaceMono-Regular.ttf
├── src/
│   └── app/
│       └── _layout.tsx (Font Loading Implementation)
└── webpack.config.js (Web Bundler Configuration)
```

## ⚙️ Konfigurasi Bundler

### Webpack (Web)
File `webpack.config.js` telah dikonfigurasi untuk menangani file font (`.ttf`, `.woff`, dll) sebagai `asset/resource`.

```javascript
// webpack.config.js
module.exports = async function (env, argv) {
  const config = await createExpoWebpackConfigAsync(env, argv);
  config.module.rules.push({
    test: /\.(woff|woff2|eot|ttf|otf)$/i,
    type: 'asset/resource',
    generator: {
      filename: 'fonts/[name][ext]',
    },
  });
  return config;
};
```

### Dependencies
Pastikan package berikut terinstall:
- `expo-font`: Core font loading utility.
- `file-loader` & `url-loader`: Webpack loaders untuk menangani aset statis.

## 🛠️ Implementasi Robust Loading
Di `_layout.tsx`, font dimuat secara manual menggunakan `Font.loadAsync` di dalam blok `try-catch` untuk menangani kegagalan loading dengan graceful fallback.

```typescript
try {
  await Font.loadAsync({
    SpaceMono: require('../../assets/fonts/SpaceMono-Regular.ttf'),
  });
} catch (e) {
  console.warn('Font loading error:', e);
} finally {
  setLoaded(true);
}
```

## ⚠️ Troubleshooting Guide
1. **Error: Unable to resolve module**: Cek path import. Pastikan menggunakan `../../assets/fonts/` jika dari `src/app/`.
2. **Font tidak muncul di Web**: Pastikan `webpack.config.js` ada dan terkonfigurasi dengan benar.
3. **Crash saat startup**: Cek console logs. Implementasi `try-catch` akan mencegah white screen of death, namun font mungkin fallback ke default system font.
