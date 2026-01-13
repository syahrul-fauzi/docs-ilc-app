# 🌐 F07: Community Hub

## 📝 Deskripsi
Platform media sosial hukum yang memungkinkan pengguna untuk berbagi kasus hukum, berdiskusi, dan mendapatkan wawasan berbasis AI (*AI Insights*) dari tren komunitas.

## 🚀 Fitur Utama

### 1. Legal Knowledge Sharing
- **Smart Tagging**: Sistem secara otomatis menambahkan tag relevan (seperti "Smart City") berdasarkan konten judul dan deskripsi kasus.
- **Case Highlights**: Menampilkan poin-poin penting dari kasus hukum untuk memudahkan pemahaman.
- **AI Insight Integration**: Pengguna dapat menyertakan hasil analisis AI ke dalam postingan komunitas.

### 2. Community Feed
- **Real-time Updates**: Feed dinamis yang menampilkan kasus hukum terbaru dari seluruh Indonesia.
- **Semantic Filtering**: Memungkinkan pengguna mencari diskusi berdasarkan topik hukum spesifik.

### 3. AI Trending Insights
- **Concept**: AI menganalisis ribuan diskusi di feed untuk mengidentifikasi tren hukum terkini.
- **Logic**: Menggunakan `CommunityService.getTrendingInsights()` untuk menghasilkan ringkasan otomatis.
- **Metrics**: Menyertakan *Trend Score* untuk menunjukkan tingkat relevansi topik.

## ⚙️ Spesifikasi Teknis

### Logic Service
- **`CommunityService.ts`**: Menangani logika bisnis untuk berbagi kasus, auto-tagging, dan pengambilan feed.
- **`ICommunityRepository`**: Antarmuka untuk penyimpanan data (SQL/Firebase).

### Analytics Events
- `community_case_shared`: Dilacak setiap kali pengguna membagikan pengetahuan hukum.
  - Properti: `caseId`, `tags`, `hasAIInsight`.

## 📱 UI/UX States
- **Feed View**: Daftar kartu kasus dengan tag visual dan ringkasan singkat.
- **Share Form**: Input minimalis dengan saran tag otomatis.
- **Insight Dashboard**: Visualisasi tren hukum yang sedang hangat dibicarakan.

## ✅ Acceptance Criteria
- [x] Mendukung pembagian kasus dengan auto-tagging berbasis kata kunci.
- [x] Integrasi dengan sistem analitik untuk melacak kontribusi pengguna.
- [x] AI mampu menghasilkan ringkasan tren dari data feed komunitas.
- [x] Mendukung penyematan (*sharing*) jawaban AI ke dalam feed komunitas.
