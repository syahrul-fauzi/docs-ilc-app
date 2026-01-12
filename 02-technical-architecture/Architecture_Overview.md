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

## 🗺️ High Level Flow
Mobile App <-> API Gateway <-> Backend Services (NestJS) <-> AI Engine & Vector DB