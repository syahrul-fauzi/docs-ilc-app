# 📂 Folder Structure (Hybrid FSD + DDD)

Aplikasi ini menggunakan struktur folder yang terorganisir berdasarkan **Feature-Sliced Design (FSD)** dengan sentuhan **Domain-Driven Design (DDD)** untuk skalabilitas.

```
/src
  /app            # Expo Router (Navigation & Layouts)
  /features       # Business Features (AI Chat, Consult, Community)
    /[feature]
      /ui         # Feature-specific components
      /model      # Feature-specific state (Context API)
      /api        # Feature-specific API calls
  /entities       # Domain Entities (User, Lawyer, Document)
    /[entity]
      /model      # Entity types & interfaces
      /service    # Core domain logic & services
  /libs           # Infrastructure & Global Utilities
    /hooks        # Global custom hooks
    /utils        # Pure utility functions
    /index.ts     # Entry point for core infrastructure (Socket, Storage, etc.)
  /shared         # Shared UI Primitives & Global Config
    /components   # Atomic UI components (Buttons, Inputs)
    /context      # Cross-cutting global contexts (Settings, Theme)
    /i18n         # Localization setup
  /widgets        # Complex UI blocks composed from features
```
