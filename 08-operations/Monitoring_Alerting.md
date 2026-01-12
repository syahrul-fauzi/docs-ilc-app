# 📊 Monitoring & Alerting (Technical Scalability)

Sistem monitoring dirancang untuk memastikan performa tinggi, reliabilitas, dan skalabilitas saat melayani jutaan pengguna di region ASEAN.

## 🔭 1. Observability Strategy (OpenTelemetry)
Kami menggunakan standar **OpenTelemetry** untuk pengumpulan data observabilitas yang agnostik terhadap vendor.

- **Distributed Tracing**: Melacak request dari mobile app -> API Gateway -> Microservices -> LLM. Berguna untuk mengidentifikasi bottleneck latensi.
- **Metrics**: Pengumpulan metrik sistem (CPU, RAM, DB Connections) dan metrik bisnis (Search Success Rate, Conversion Rate).
- **Logs**: Logging terpusat dengan level yang sesuai (Info, Warn, Error). Log PII (Personal Identifiable Information) harus disamarkan secara otomatis.

## ⚡ 2. Performance Optimization
- **Edge Caching**: Menggunakan Cloudflare/Vercel Edge untuk menyajikan konten statis dan respons AI yang sering dicari berdasarkan lokasi geografis.
- **LLM Latency Monitoring**: Melacak waktu respon dari penyedia LLM (OpenAI/Anthropic). Implementasi fallback ke model yang lebih ringan jika latensi > 5 detik.
- **Mobile Performance**: Monitoring ukuran bundle aplikasi, waktu startup, dan penggunaan baterai/data.

## 🛡️ 3. Reliability & Resilience
- **SLO-based Alerting**: Notifikasi dikirim berdasarkan *Service Level Objectives* (misal: 99.9% uptime, 95% response < 200ms).
- **Circuit Breaker**: Mencegah kegagalan sistem merembet jika salah satu service (mis: Payment Gateway) sedang down.
- **Offline Mode (Basic)**: Memastikan user tetap bisa membaca konten yang sudah di-cache saat koneksi internet tidak stabil.

## 🚨 4. Alerting Policy
- **Critical (Slack & PagerDuty)**:
  - API Error Rate > 2% dalam 5 menit.
  - Database connection exhaustion.
  - LLM API key usage spike / quota limit.
- **Warning (Slack)**:
  - Peningkatan latensi API > 500ms.
  - Penurunan drastis pada Conversion Rate harian.
  - Low disk space pada server.
