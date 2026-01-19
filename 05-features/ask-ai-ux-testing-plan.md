# 🧪 Rencana Pengujian Usability & Estimasi ROI: Ask AI

Dokumen ini merinci strategi pengujian (**Test**) dari Design Thinking dan evaluasi (**Evaluate**) dari The Wheel Method untuk fitur Ask AI di ILC-APP.

---

## 1. Metodologi Pengujian (Design Thinking: Test)

### 1.1 Peserta & Skenario
- **Target**: 20 Peserta (10 Advokat Senior, 10 Paralegal).
- **Metode**: *Moderated Think-Aloud* dan *Post-Task Interview*.
- **Skenario Utama**:
    1.  **Analisis Dokumen**: "Unggah foto surat gugatan ini dan identifikasi 3 risiko hukum utama dalam 30 detik."
    2.  **Riset Yurisprudensi**: "Cari putusan MA terkait wanprestasi yang memiliki *Confidence Score* > 90%."
    3.  **Intervensi Agen**: "Saat AI sedang meriset, ubah mode penalaran menjadi 'Creative' untuk mencari argumen alternatif."

### 1.2 Metrik Keberhasilan
| Metrik | Instrumen | Target (2026) |
| :--- | :--- | :--- |
| **Usability** | System Usability Scale (SUS) | **> 82 (Grade A)** |
| **Task Ease** | Single Ease Question (SEQ) | **> 6.5 / 7** |
| **Explainability** | User Understanding Score | **> 90%** (Pengguna paham mengapa AI memberi jawaban tersebut) |
| **Trust Level** | Verification Click-rate | **> 75%** (Pengguna mengklik link JDIH untuk verifikasi) |

---

## 2. Evaluasi Efektivitas & ROI (The Wheel Method: Evaluate)

### 2.1 Pengukuran ROI (Return on Investment)
Kami memproyeksikan efisiensi biaya dan waktu bagi firma hukum yang mengadopsi ILC-APP:

| Aktivitas | Metode Tradisional | Dengan ILC-APP (Ask AI) | Efisiensi (ROI) |
| :--- | :--- | :--- | :--- |
| **Riset Regulasi** | 120 Menit | 15 Menit | **87.5%** |
| **Review Kontrak** | 180 Menit | 45 Menit | **75%** |
| **Penyusunan Somasi** | 60 Menit | 10 Menit | **83.3%** |

**Estimasi Penghematan Biaya**: 
Dengan asumsi tarif rata-rata advokat Rp 2.000.000/jam, penggunaan ILC-APP dapat menghemat hingga **Rp 15.000.000 per kasus** melalui otomatisasi tugas rutin.

### 2.2 Siklus Iterasi (The Wheel Loop)
Berdasarkan hasil evaluasi Q1 2026:
- **Jika SUS < 80**: Lakukan audit ulang pada *Information Architecture* di [AskInputZone.tsx](file:///home/inbox/smart-ai/lawyers-hub/apps/ilc-app/src/features/ai-chat/ui/AskInputZone.tsx).
- **Jika Akurasi < 95%**: Tingkatkan parameter *Grounded Search* pada `ResearcherAgent`.
- **Jika Latensi > 60 detik**: Implementasikan model SLM (Small Language Models) untuk tugas-tugas ringan.

## 3. Feedback Loop & Continuous Improvement

### 3.1 Mekanisme Umpan Balik Pengguna
- **Direct Feedback**: Tombol 👍/👎 pada setiap respons AI dengan modal opsional untuk alasan spesifik (misal: "Halusinasi", "Outdated", "Terlalu Umum").
- **Correction Tool**: Pengguna dapat memperbaiki kutipan undang-undang yang salah secara langsung, yang akan masuk ke antrean *Human-in-the-loop* (HITL) untuk pelatihan ulang model.
- **Usage Analytics**: Pelacakan fitur yang paling sering digunakan dan yang sering menyebabkan *drop-off* menggunakan `analytics.ts`.

### 3.2 Roadmap Evaluasi Berkala
1.  **Bi-weekly Quality Audit**: Review manual 5% dari total interaksi AI oleh pakar hukum internal.
2.  **Monthly A/B Testing**: Pengujian variasi UI pada [ThoughtStream](file:///home/inbox/smart-ai/lawyers-hub/apps/ilc-app/src/features/ai-chat/ui/ThoughtStream.tsx) untuk meningkatkan *User Engagement*.
3.  **Quarterly ROI Review**: Penyesuaian metrik penghematan waktu berdasarkan data penggunaan riil di lapangan.

---
*Dikelola oleh Tim Lawyers Hub - Update Terakhir: 2026-01-19*
