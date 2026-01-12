# Product Requirements (ILC-APP)

## Vision
Menjadi platform hukum AI #1 di Indonesia dan ASEAN yang menyediakan solusi hukum instan, terpercaya, dan mudah diakses melalui teknologi AI canggih dan jaringan pengacara profesional.

## Problems
- **Informasi Hukum Terfragmentasi**: Sulitnya menemukan dasar hukum yang tepat dan terkini bagi masyarakat awam.
- **Hambatan Akses & Biaya**: Konsultasi hukum seringkali dianggap mahal dan sulit dijangkau.
- **Kurangnya Kepercayaan pada AI**: Pengguna membutuhkan bukti validitas (pasal/sumber) atas jawaban yang diberikan oleh AI.

## Success Metrics
| Kategori | Metrik | Target |
| :--- | :--- | :--- |
| **Growth** | DAU | ≥ 5.000 dalam 3 bulan pertama |
| **Retention** | D7 Retention | ≥ 30% |
| **Conversion** | Search → Consult | ≥ 8% |
| **Monetization** | Conversion Rate (Premium) | 3-5% dalam 6 bulan |

## Core Features
### 1. Advanced AI Legal Experience
- **AI Search & Answer**: Menggunakan *Vector Search* dan *LLM Reranking*.
- **Answer Trust Signals**: Menampilkan *Confidence Score*, *Source Badges*, dan tautan langsung ke pasal UU.
- **Contextual Prompting**: Adaptasi gaya komunikasi (formal/konsultatif) dan integrasi konteks hukum lokal.

### 2. Engagement Loop
- **Daily/Weekly Legal Digest**: Notifikasi konten hukum populer dan edukasi harian.
- **Community Feed**: Wadah interaksi melalui *Case Highlights* dan *Q&A Threads*.
- **Gamification**: Sistem *Leaderboards* dan *Badges* untuk pengguna dan kontributor aktif.

### 3. Consultation & Monetization
- **Dynamic Matching & Pricing**: Pencocokan pengacara berdasarkan spesialisasi dengan harga dinamis.
- **Subscription Models**: Tier *Free* (terbatas) dan *Premium* (unlimited search + diskon konsultasi).
- **In-App Payment**: Integrasi gerbang pembayaran lokal (GoPay, OVO, Bank Transfer).

## Technical Requirements
- **Observability**: Distributed Tracing (OpenTelemetry) dan monitoring berbasis SLO.
- **Performance**: LLM Caching, Edge Caching, dan optimisasi bundle mobile.
- **Regional Ready**: Infrastruktur yang mendukung multi-yurisdiksi (ASEAN Expansion).
