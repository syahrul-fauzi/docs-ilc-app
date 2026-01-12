# 📡 Panduan Monitoring & Observabilitas ILC-APP

Dokumen ini menjelaskan strategi monitoring, *alerting*, dan penanganan insiden untuk memastikan ketersediaan dan performa ILC-APP.

---

## 1. Arsitektur Monitoring

Kami menggunakan pendekatan *Observability-Driven Development* dengan tiga pilar utama:

### 1.1 Logging (Terstruktur)
- **Library**: `LoggerService` (Custom wrapper).
- **Format**: JSON terstruktur dengan *severity levels* (INFO, WARN, ERROR, DEBUG).
- **Context**: Setiap log mencakup `taskId`, `userId`, `tenantId`, dan `timestamp`.
- **Audit Trail**: Mencatat setiap langkah keputusan Agent AI untuk transparansi hukum.

### 1.2 Metrics (Kuantitatif)
- **AI Performance**:
  - `evalScore`: Kualitas jawaban AI (Target > 0.7).
  - `latency`: Waktu respons (Target < 15s untuk complex queries).
  - `tokenUsage`: Efisiensi biaya.
- **Business Metrics**:
  - `conversion_rate`: Rasio user gratis ke berbayar.
  - `churn_rate`: Tingkat pembatalan langganan.

### 1.3 Tracing (Distribusi)
- Melacak perjalanan request dari Mobile App -> API Gateway -> AI Agent -> Database.
- Identifikasi *bottleneck* pada integrasi eksternal (misal: API BPN lambat).

---

## 2. Strategi Alerting

Sistem peringatan dikonfigurasi untuk mendeteksi anomali kritis:

| Severity | Trigger Condition | Action |
| :--- | :--- | :--- |
| **CRITICAL** | `evalScore` < 0.5 selama 5 menit berturut-turut | Notifikasi Tim Engineer (PagerDuty) & Fallback ke Mode Manual |
| **HIGH** | Latensi rata-rata > 30s | Notifikasi Tim Dev (Slack) |
| **MEDIUM** | API Eksternal (BPN/MA) down | Log Error & Tampilkan pesan "Sumber Data Terbatas" ke User |
| **LOW** | Percobaan login gagal > 10x/menit | Flag akun & Notifikasi Keamanan |

---

## 3. Runbook: Penanganan Insiden

### Skenario 1: Kualitas Jawaban AI Menurun (`evalScore` rendah)
1. **Verifikasi**: Cek Dashboard Analytics, filter berdasarkan model AI yang aktif.
2. **Isolasi**: Jika spesifik pada satu model, ganti konfigurasi via `ConfigService` untuk menggunakan model cadangan.
3. **Analisis**: Periksa `MemoryService` untuk melihat apakah ada pola input user yang baru/tidak dikenali.
4. **Perbaikan**: Update *System Prompt* atau tambahkan contoh kasus baru ke *Knowledge Base*.

### Skenario 2: Kegagalan Integrasi Pembayaran
1. **Cek Log**: Filter log dengan `event: conversion_failed`.
2. **Validasi Vendor**: Cek status page penyedia Payment Gateway (Xendit/Midtrans).
3. **Mitigasi**: Aktifkan metode pembayaran alternatif jika tersedia.

---

## 4. Setup Tools (Rekomendasi)

Untuk lingkungan produksi, integrasikan dengan:
- **Sentry**: Untuk *Error Tracking* & *Crash Reporting* (React Native).
- **Prometheus + Grafana**: Untuk visualisasi metrik server & AI.
- **ELK Stack (Elasticsearch, Logstash, Kibana)**: Untuk sentralisasi log.

---
*Dikelola oleh Tim DevOps Lawyers Hub*
