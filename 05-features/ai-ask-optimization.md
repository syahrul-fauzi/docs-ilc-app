# AI Ask Feature Optimization

Dokumen ini mencatat optimasi yang dilakukan pada fitur Ask (AI Chat) untuk mencapai pengalaman pengguna yang setara dengan ChatGPT.

## 1. Perubahan Arsitektur Chat

### 1.1 Inverted FlatList
Kami mengubah implementasi `FlatList` menjadi `inverted={true}` pada `AskScreen`.
- **Manfaat**: Auto-scroll ke pesan terbaru secara alami (pesan terbaru berada di index 0, di bagian bawah layar).
- **Penyesuaian**: Logika state management di `AiChatContext` diubah untuk menggunakan `prepend` (`[newMessage, ...prev]`) alih-alih `append`.

### 1.2 Sticky Input Zone
Komponen `AskInputZone` kini bersifat sticky di bagian bawah layar, memberikan akses cepat untuk input tanpa terganggu oleh scroll pesan.

## 2. Peningkatan Fitur

### 2.1 Multi-turn Conversation
Mendukung percakapan multi-turn dengan manajemen state yang konsisten. Fitur `editMessage` memungkinkan pengguna untuk mengubah pertanyaan sebelumnya, yang secara otomatis akan menghapus pesan setelahnya dan memulai aliran percakapan baru dari titik tersebut.

### 2.2 Typing Indicator
Integrasi `TypingIndicator` yang dioptimalkan untuk performa. Menggunakan animasi yang halus dengan fallback untuk perangkat dengan spesifikasi rendah.

### 2.3 Debounced Storage
Penyimpanan riwayat pesan ke storage lokal kini menggunakan debounce (1 detik) untuk mencegah operasi I/O yang berlebihan saat pesan diterima secara streaming.

## 3. Perbaikan Teknis

### 3.1 Syntax & Type Errors
- Memperbaiki `SyntaxError` pada `AskInputZone.tsx` terkait tag JSX yang tidak tertutup.
- Memperbaiki error `TS2552` dengan mengimpor modul `storage` yang hilang.

### 3.2 Pagination Logic
`ChatHistoryRepository` telah disesuaikan untuk menangani paginasi pada urutan pesan terbalik (inverted), memastikan `loadMore` memuat pesan yang lebih lama di bagian atas daftar.

---
*Terakhir diperbarui: 2026-01-20*
