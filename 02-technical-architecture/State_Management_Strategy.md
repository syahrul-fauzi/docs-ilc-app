# 🧠 State Management Strategy

## 🌐 Server State
Menggunakan pola **Service-based DDD** di folder `entities/` untuk fetching dan sinkronisasi data. Ke depannya dapat diintegrasikan dengan **@tanstack/react-query** untuk optimasi caching.

## 📱 Client State (Global & Feature)
Kami menggunakan **React Context API** secara modular untuk mengelola state aplikasi.

### 1. Global Context
Digunakan untuk data yang dibutuhkan di seluruh aplikasi. Terletak di `src/shared/context/` atau `src/libs/`.
- **AuthContext**: Status autentikasi dan data user.
- **SettingsContext**: Preferensi bahasa, tema (dark/light), dan notifikasi.
- **ThemeContext**: Konfigurasi styling UI.

### 2. Feature Context
Digunakan untuk data yang terisolasi di dalam satu fitur tertentu. Terletak di `src/features/[feature]/model/`.
- **AiChatContext**: History chat aktif dan status streaming AI.
- **CommunityContext**: Feed postingan dan filter komunitas.

## 🧩 Local State
Untuk state yang hanya relevan bagi satu komponen (misal: input form, status modal lokal), tetap gunakan `useState` atau `useReducer` standar React.
