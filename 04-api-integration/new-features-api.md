# 🚀 New AI Features API Documentation

Dokumen ini merinci API internal untuk fitur baru: Regional Switcher, Voice-to-Legal, dan AI Legal Health Check.

---

## 1. RegionService
Layanan untuk mengelola yurisdiksi hukum dan preferensi regional.

### `getSelectedJurisdiction(): Promise<JurisdictionId | null>`
Mengambil ID yurisdiksi yang dipilih pengguna dari penyimpanan lokal.

### `setSelectedJurisdiction(id: JurisdictionId): Promise<void>`
Menyimpan pilihan yurisdiksi pengguna dan mencatat aktivitas audit.

### `detectJurisdiction(query: string): JurisdictionId`
Menganalisis teks kueri untuk mendeteksi yurisdiksi secara otomatis.

---

## 2. VoiceService
Layanan untuk pemrosesan suara dan enkripsi rekaman hukum.

### `transcribeAudio(audioUri: string): Promise<VoiceTranscription>`
Mengirimkan URI audio untuk ditranskripsi menjadi teks dengan penandaan entitas hukum.
- **Return**: `{ text: string, confidence: number, entities: string[] }`

### `encryptRecording(audioUri: string): Promise<string>`
Mengamankan rekaman suara dengan enkripsi end-to-end sebelum dikirim/disimpan.

---

## 3. LegalHealthCheckService
Layanan analisis risiko hukum berbasis AI.

### `analyzeRisk(documentIds: string[]): Promise<RiskAnalysis>`
Menganalisis kumpulan dokumen untuk menentukan skor kesehatan hukum dan temuan risiko.
- **Return**: `RiskAnalysis` (skor, ringkasan, daftar risiko).

### `exportReport(analysis: RiskAnalysis, format: 'pdf' | 'docx'): Promise<string>`
Menghasilkan laporan formal dalam format PDF atau DOCX.

---

## Audit Logging Standard
Semua fitur baru mengadopsi standar logging audit di `src/shared/libs/logger.ts`:
- **Format**: `[Audit] <Action Description>`
- **Metadata**: Menyertakan `timestamp`, `action_id`, dan context yang relevan.
