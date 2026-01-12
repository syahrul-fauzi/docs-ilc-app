# Workspace Optimization — ILC-APP

Dokumen ini berisi evaluasi struktur folder saat ini dan rekomendasi organisasi workspace yang lebih terstruktur untuk mendukung skalabilitas dan kemudahan pemeliharaan.

## 1. Evaluasi Struktur Saat Ini
Struktur repositori saat ini mengikuti pola standar Expo/React Native dengan folder utama di root:
- `app/`: Routing dengan Expo Router.
- `components/`, `hooks/`, `services/`, `context/`: Berisi file yang dikelompokkan berdasarkan jenis teknisnya.
- **Masalah Potensial**: Seiring bertambahnya fitur, folder-folder ini akan menjadi sangat besar dan sulit dikelola karena file dari berbagai fitur bisnis tercampur dalam satu folder (misal: hook untuk 'Chat' dan hook untuk 'Auth' ada di satu folder `hooks/`).

## 2. Rekomendasi Struktur Workspace (Hybrid Modular)
Kami merekomendasikan transisi ke arsitektur **Feature-Slice-Driven (FSD)** yang dikombinasikan dengan **Domain-Driven Design (DDD)**. Kode akan dikelompokkan berdasarkan **Fitur Bisnis**, bukan jenis file teknis.

### Diagram Struktur Folder Optimal
```text
/
├── app/                  # Routing & Layouts (Expo Router)
├── assets/               # Static assets (images, fonts)
├── src/                  # Sumber kode utama (Recommended move from root)
│   ├── features/         # Feature slices (Business logic modules)
│   │   ├── ask/          # Fitur "Tanya AI"
│   │   ├── chat/         # Fitur "Komunitas/Feed"
│   │   └── consult/      # Fitur "Konsultasi Hukum"
│   ├── entities/         # Shared domain entities (User, Case, Tenant)
│   ├── shared/           # Cross-feature code
│   │   ├── ui/           # Generic UI components (Ag-UI wrappers)
│   │   ├── hooks/        # Utility hooks
│   │   └── utils/        # Helper functions
│   └── libs/             # External integration (apiClient, navigation)
├── docs/                 # Dokumentasi proyek (Terstruktur)
├── config/               # Konfigurasi aplikasi & environment
└── scripts/              # Automation & Validation scripts
```

## 3. Konvensi Penamaan Konsisten

### File & Folder
- **Folders**: `kebab-case` (contoh: `feature-ask`, `auth-service`).
- **Components**: `PascalCase` (contoh: `PrimaryButton.tsx`, `ChatListItem.tsx`).
- **Hooks**: `camelCase` dengan prefix `use` (contoh: `useAuth.ts`, `useCommunityFeed.ts`).
- **Utilities/Services**: `camelCase` (contoh: `apiClient.ts`, `logger.ts`).
- **Types/Interfaces**: `PascalCase` (contoh: `UserEntity.ts`, `ApiResponse.ts`).

### Kode (TypeScript)
- **Variables & Functions**: `camelCase`.
- **Constants**: `UPPER_SNAKE_CASE`.
- **Classes**: `PascalCase`.
- **Enums**: `PascalCase` untuk nama, `UPPER_SNAKE_CASE` untuk nilai.

## 4. Langkah Implementasi
1. Buat folder `src/` dan pindahkan folder inti (`components`, `hooks`, `services`, `context`) ke dalamnya secara bertahap.
2. Identifikasi kode yang bersifat fitur spesifik dan pindahkan ke `src/features/[feature-name]`.
3. Perbarui `tsconfig.json` paths untuk memudahkan import (misal: `@features/*`, `@shared/*`).
