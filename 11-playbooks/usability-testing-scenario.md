# Skenario Usability Testing - ILC-APP

## 1. Pendahuluan
Dokumen ini merinci skenario pengujian untuk memvalidasi alur konsultasi AI baru dan fitur editor kolaboratif pada ILC-APP.

## 2. Profil Peserta
- **Target**: 10-15 Pengguna
- **Segmentasi**:
  - 5 Pengacara Profesional (Legal Expert)
  - 5 Mahasiswa Hukum (Aspiring Lawyers)
  - 5 Masyarakat Umum (General Public)

## 3. Skenario Pengujian

### Skenario A: Inisiasi Konsultasi Hukum AI
1. Buka aplikasi ILC-APP.
2. Navigasi ke tab "Ask AI".
3. Ajukan pertanyaan hukum: *"Bagaimana prosedur cerai gugat bagi PNS?"*
4. Verifikasi apakah jawaban AI relevan dan menyertakan referensi undang-undang yang tepat.
5. Gunakan fitur "Tindak Lanjut" untuk memperdalam pertanyaan.

**Metrik:**
- Waktu penyelesaian (Inisiasi -> Jawaban diterima)
- Tingkat keberhasilan (User merasa puas dengan jawaban)

### Skenario B: Penyusunan Dokumen (Collaborative Editor)
1. Dari hasil konsultasi, pilih opsi "Drafting Dokumen".
2. Gunakan template "Surat Kuasa".
3. Lakukan pengeditan pada teks (verifikasi keterbacaan font Inter 12pt).
4. (Hanya Tablet) Aktifkan mode multi-kolom untuk melihat AI Insights di samping editor.
5. Simpan versi dokumen.

**Metrik:**
- Kemudahan navigasi template
- Keterbacaan teks (Skala 1-5)
- Efektivitas layout multi-kolom pada tablet

### Skenario C: Feedback Loop & AI Insights
1. Gunakan fitur "AI Suggest" di editor.
2. Review saran yang diberikan oleh AI di panel samping.
3. Berikan rating pada jawaban AI untuk membantu peningkatan akurasi di masa depan.

**Metrik:**
- Relevansi saran AI
- Kejelasan UI Feedback

## 4. Pengumpulan Data
- **Kuantitatif**: Waktu (detik), Success Rate (%), Rating (1-5).
- **Kualitatif**: Feedback verbal, ekspresi wajah (via observasi), keluhan spesifik.

## 5. Iterasi Desain
Hasil dari pengujian ini akan dianalisis untuk menentukan:
- Perbaikan ukuran font atau kontras warna.
- Penyesuaian proporsi kolom pada layout tablet.
- Penyederhanaan alur chat AI jika dirasa terlalu kompleks.
