# ILC-APP (Indonesia Lawyers Club)

Selamat datang di repositori **ILC-APP**, aplikasi mobile/web berbasis AI yang dirancang untuk merevolusi akses hukum di Indonesia.

## 📚 Dokumentasi
Dokumentasi lengkap proyek ini disusun secara sistematis untuk memudahkan pengembangan dan pemeliharaan.

### 🚀 Mulai Cepat (Quick Start)
1. **Prasyarat**: Node.js v18+, npm/yarn.
2. **Instalasi**:
   ```bash
   npm install
   ```
3. **Menjalankan Development Server**:
   ```bash
   npx expo start
   ```
4. **Testing**:
   ```bash
   npm test
   ```

### 📖 Panduan Lengkap
Silakan akses dokumen berikut untuk detail teknis dan standar operasional:

- [**📜 Aturan Proyek Utama (Project Rules)**](../.trae/rules/project_rules.md): Standar pengembangan, kualitas, dan operasional resmi.
- [**🏗️ Arsitektur Hybrid FSD-DDD**](../.trae/rancangan%20implementasi%20FSD-DDD-Hybrid%20versi%20“next-generation”.md): Panduan struktur kode generasi terbaru.
- [**00-overview**](docs/00-overview/README.md): Visi, Misi, dan Cakupan Proyek.
- [**01-product**](docs/01-product/README.md): Product Requirements Document (PRD).
- [**02-technical-architecture**](docs/02-technical-architecture/README.md): Diagram sistem dan struktur data.
- [**03-mobile-implementation**](docs/03-mobile-implementation/README.md): Standar pengembangan UI/UX dengan Expo.
- [**05-features**](docs/05-features/README.md): Dokumentasi detail fitur-fitur utama.
  - [01-AI Legal Engine](docs/05-features/01-ai-legal-engine.md)
  - [02-Community Hub](docs/05-features/02-community-hub.md)
  - [03-Legal Tools](docs/05-features/03-legal-tools.md)
  - [04-Billing & Subscription](docs/05-features/04-billing-subscription.md)
  - [05-Notification System](docs/05-features/05-notification-system.md)
  - [06-Generative UI & Collaboration](docs/05-features/06-generative-ui-collaboration.md)
- [**11-playbooks**](docs/11-playbooks/): Panduan operasional ("How-to") dan pemecahan masalah.
  - [**Arsitektur Layanan**](docs/11-playbooks/01-service-architecture.md): Detail implementasi backend-for-frontend.
  - [**Fixing Navigation**](docs/11-playbooks/navigation_fix.md): Troubleshooting React Navigation.

## 🏗️ Arsitektur Proyek: Hybrid FSD-DDD Versi "Next-Generation"

Proyek ini menggunakan arsitektur **Hybrid FSD-DDD (Feature-Sliced Design + Domain-Driven Design)** yang dioptimalkan untuk aplikasi mobile AI-native.

### Struktur Arsitektur & Alur Data

```mermaid
graph TB
    subgraph "Application Layer (Processes)"
        LIP[LegalInquiryProcess]
    end

    subgraph "Domain Layer (Entities)"
        AE[AI Entity]
        CE[Community Entity]
        BE[Billing Entity]
        UE[User Entity]
        DE[Document Entity]
        NE[Notification Entity]
    end

    subgraph "Infrastructure Layer (Shared)"
        SL[Shared Libs: Logger, Analytics, API]
        SS[Shared Services: Storage, Config]
    end

    LIP --> AE
    LIP --> BE
    LIP --> CE
    
    AE --> SL
    AE --> SS
    BE --> SL
    CE --> SL
    DE --> SS
    NE --> SL

    AE -.->|Continuous Learning| SS
    BE -.->|Payment Logs| SL
```

### Layer Utama (FSD Layers)

```mermaid
graph TD
    App[src/app: Routing & Providers] --> Processes[src/processes: Workflows]
    Processes --> Pages[src/pages: Screens]
    Pages --> Widgets[src/widgets: Large UI Blocks]
    Widgets --> Features[src/features: User Actions]
    Features --> Entities[src/entities: Domain Logic]
    Entities --> Shared[src/shared: Infrastructure]
```

- **`src/app`**: Routing (Expo Router) dan entry point aplikasi.
- **`src/processes`**: Alur bisnis kompleks lintas fitur (misal: AI Drafting Flow).
- **`src/pages`**: Komposisi layar utuh (Screen Components).
- **`src/widgets`**: Komponen UI besar & mandiri (misal: LegalFeed, ChatWindow).
- **`src/features`**: Aksi pengguna yang spesifik (misal: `auth`, `ai-chat`, `legal-search`).
- **`src/entities`**: Logika bisnis inti berbasis **Bounded Context** (misal: `ai`, `user`, `billing`, `lawyer`, `case`).
- **`src/shared`**: Komponen UI atomik (Ag-UI), API client (Axios/Socket), hooks, dan utilitas generik (Logger, Error).

### Agentic Lifecycle (Next-Gen AI)
Sistem mengadopsi siklus hidup otonom untuk penyelesaian masalah hukum:
1. **Planning**: Memecah pertanyaan kompleks menjadi langkah-langkah kecil.
2. **Context Gathering**: Mengumpulkan rujukan hukum dan memori masa lalu.
3. **Analysis**: Sintesis data oleh AI Specialist (Analyst Agent).
4. **Action**: Memberikan jawaban dan menyiapkan langkah aksi (Generative UI).
5. **Self-Evaluation**: Validasi akurasi jawaban sebelum ditampilkan.

### Prinsip Pengembangan
1. **Domain Centric**: Logika bisnis murni harus berada di dalam `src/entities`.
2. **Inward Dependency**: Layer yang lebih luar (App/Pages/Features) bergantung pada layer yang lebih dalam (Entities/Shared), bukan sebaliknya.
3. **Ubiquitous Language**: Menggunakan terminologi hukum yang konsisten (misal: `LegalInquiry`, `TrustSignals`).
4. **Agentic Workflow**: Mendukung orkestrasi agen AI secara otonom di layer domain.

Untuk detail lebih lanjut mengenai implementasi, silakan baca [Rancangan Implementasi FSD-DDD-Hybrid](../.trae/rancangan%20implementasi%20FSD-DDD-Hybrid%20versi%20“next-generation”.md).

---

## 🏗️ Fitur Utama

### 1. AI Legal Engine
Menggunakan **Agentic Workflow** untuk memberikan jawaban hukum yang akurat dengan *Trust Signals* (sumber terverifikasi).

### 2. Community Hub
Platform sosial untuk diskusi kasus, berbagi wawasan, dan *networking* antar profesional hukum.

### 3. Smart Document Drafting
Editor kolaboratif (Yjs) untuk menyusun dokumen hukum secara real-time.

## 🛡️ Keamanan & Kualitas

### Standar Pengembangan
- **Type Safety**: TypeScript Strict Mode.
- **Linting**: ESLint + Prettier.
- **Testing**: Jest (Unit) + Maestro (E2E).
- **Error Handling**: Interceptor terpusat dengan normalisasi error.

### Keamanan
- **Auth**: JWT dengan rotasi token otomatis.
- **Data**: Enkripsi end-to-end untuk konsultasi privat.
- **Compliance**: Mengikuti standar perlindungan data pribadi (UU PDP).

---
*Dibuat dengan ❤️ oleh Tim Smart AI Lawyers Hub*
