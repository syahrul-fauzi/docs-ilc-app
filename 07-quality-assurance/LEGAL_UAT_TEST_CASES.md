# ⚖️ Skenario Uji Coba Tim Legal (UAT)

Dokumen ini berisi daftar kasus uji (test cases) untuk divalidasi oleh tim legal di lingkungan staging.

## 1. Modul AI Document Analysis
| ID | Skenario | Hasil yang Diharapkan |
|:---|:---|:---|
| L-01 | Analisis Surat Kuasa Khusus | AI mendeteksi "Kuasa Khusus" dan menyarankan klausul hak substitusi. |
| L-02 | Analisis Akta Notaris | AI memvalidasi komparisi dan mengingatkan risiko degradasi akta jika saksi tidak lengkap. |
| L-03 | Deteksi Klausul SHA | AI menyarankan mekanisme *Deadlock Resolution* pada draf perjanjian pemegang saham. |

## 2. Modul Collaborative Editor
| ID | Skenario | Hasil yang Diharapkan |
|:---|:---|:---|
| E-01 | Smart Formatting | AI secara otomatis merapikan format Pasal dan kapitalisasi judul dokumen. |
| E-02 | Penjelasan Konteks Hukum | Pengguna mendapatkan definisi "Wanprestasi" yang akurat saat mengklik istilah tersebut. |
| E-03 | Real-time Risk Alert | Muncul peringatan risiko tinggi saat klausul krusial (seperti arbitrase) dihapus. |

## 3. Trust Signals & Akurasi
| ID | Skenario | Hasil yang Diharapkan |
|:---|:---|:---|
| T-01 | Verifikasi Sumber Resmi | Hasil pencarian hukum menampilkan badge "Official Government" untuk link ke JDIH. |
| T-02 | Recency Check | AI memprioritaskan regulasi terbaru (misal: UU Cipta Kerja vs UU lama). |

## Mekanisme Pelaporan
Jika ditemukan ketidaksesuaian:
1. Ambil tangkapan layar (screenshot).
2. Catat langkah reproduksi.
3. Laporkan melalui tiket di sistem pelacakan bug internal dengan label `LEGAL-FEEDBACK`.

---
*Dibuat oleh Agent - 2026-01-18*
