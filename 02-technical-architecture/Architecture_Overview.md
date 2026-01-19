# 🏗️ Architecture Overview

## Tech Stack
- **Frontend**: React Native + Expo (Managed Workflow).
- **UI Framework**: Ag-UI + Tailwind CSS (NativeWind).
- **AI/Chat**: Copilotkit + Custom Vector Database (Legal Knowledge Graph).
- **API Client**: Axios with interceptors for auth & error handling.
- **State Management**: Zustand (for global state) & React Query (for server state).

## 🚀 Scalability & Regional Readiness
### 1. Multi-Region Deployment
- Persiapan infrastruktur berbasis kontainer (Docker/K8s) untuk memudahkan *deployment* di region baru (ASEAN Expansion).
- Penggunaan CDN (Content Delivery Network) untuk meminimalkan latency aset statis di luar Indonesia.

### 2. Microservices Transition Path
- Arsitektur saat ini berbasis Modular Monolith untuk kecepatan *delivery*.
- Jalur migrasi ke Microservices untuk modul kritis seperti **Payment Gateway** dan **AI RAG Engine** guna skalabilitas independen.

### 3. Data Localization & Security
- Implementasi *data isolation* per negara untuk mematuhi regulasi perlindungan data lokal (mis: PDPA di Thailand/Malaysia).
- Enkripsi data *at rest* dan *in transit* (TLS 1.3).

## 🏗️ Core Design Principles
### 1. Hybrid FSD-DDD
- **Feature-Sliced Design (FSD)**: Organisasi kode berdasarkan domain bisnis dan fungsionalitas untuk meningkatkan keterbacaan dan pemeliharaan.
- **Domain-Driven Design (DDD)**: Fokus pada logika bisnis inti melalui *Bounded Contexts* dan *Entities*.

### 2. SOLID Service Architecture
- Penggunaan **Interfaces** untuk semua layanan inti (Billing, Community, Notification, etc.) untuk memfasilitasi pengujian dan fleksibilitas.
- **Dependency Injection**: Memungkinkan penggantian implementasi layanan tanpa mengubah logika bisnis.

### 3. Agentic AI Lifecycle
- Implementasi workflow otonom: Planning -> Context Gathering -> Analysis -> Action -> Self-Evaluation.
- Integrasi *Trust Signals* untuk menjamin akurasi hukum.

### 4. Global UI Standards (Ag-UI)
- Standarisasi elemen interaktif (Button, Pressable) dengan dukungan haptics, animasi (Reanimated), dan aksesibilitas penuh.
- Dukungan multilingual (i18n) dengan fallback Bahasa Indonesia yang cerdas.