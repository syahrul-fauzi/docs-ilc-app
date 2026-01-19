# 🤖 F01: AI Search & Answer

## 📝 Deskripsi
Fitur pencarian semantik yang memungkinkan pengguna mengajukan pertanyaan hukum dalam bahasa alami dan menerima jawaban instan berbasis AI yang didukung oleh referensi peraturan perundang-undangan Indonesia.

## 🚀 Strategi Penguatan (Advanced AI Legal Experience)

### 1. Knowledge Layer & Search Optimization
- **Legal Knowledge Graph / Vector Search Layer**: 
  - Membangun *custom vector database* yang mencakup UU, putusan pengadilan, dan artikel hukum terverifikasi.
  - Implementasi *Semantic Search* dikombinasikan dengan *LLM Reranking* untuk akurasi tertinggi.
- **Answer Trust Signals (Implementation v2)**:
  - **Confidence Score**: Menampilkan tingkat kepercayaan AI terhadap jawaban (0-100%).
  - **Official Source Badge**: Penanda khusus jika jawaban didukung oleh rujukan pemerintah (JDIH, BPN, Kemenaker).
  - **Verification Status**: Status verifikasi sistem (Verified, Partially Verified, Unverified).
  - **Recency Score**: Menilai seberapa baru regulasi yang digunakan sebagai rujukan.
  - **Source Badges**: Penanda visual untuk sumber resmi (mis: Lembaran Negara).
  - **Pasal Direct Links**: Tautan langsung ke teks spesifik dalam peraturan terkait.
  - **Ask Follow-up**: Memungkinkan *threaded conversation* untuk pendalaman materi.

### 2. Contextual Intelligence & Tone of Voice (TOV)
- **ILC Persona Lawyer Style**: AI beradaptasi dengan brand identity ILC: *Reliable, Professional, Approachable, & Actionable*.
- **TOV Guidelines**:
  - **Reliable**: Selalu menyertakan rujukan UU/PP yang valid.
  - **Professional**: Menggunakan terminologi hukum yang tepat namun tetap mudah dimengerti.
  - **Approachable**: Menggunakan kalimat pembuka yang menyambut dan penutup yang mengajak interaksi.
  - **Actionable**: Setiap jawaban harus menyertakan langkah nyata (e.g., "Hubungkan dengan pengacara" atau "Cek sertifikat ke BPN").
- **Local Context Integration**: Menyisipkan konteks hukum spesifik Indonesia (UU, Perda, Yurisprudensi) ke dalam prompt sistem.

### 3. Reasoning Transparency (The "Reasoning Path")
- **Concept**: Menampilkan proses berpikir AI secara transparan untuk meningkatkan kepercayaan pengguna melalui mekanisme orkestrasi agen.
- **Component**: `AgentOrchestrator` reasoning path.
- **Flow (Agentic Phases)**:
  1.  **Memory Retrieval**: Mencari pengalaman relevan dari interaksi sebelumnya untuk memperkaya konteks.
  2.  **Research**: Melakukan penelusuran pada database hukum dan sumber resmi (JDIH, MA, dsb).
  3.  **Domain & Persona Awareness**: Mengidentifikasi domain hukum (Pidana, Perdata, dll) dan menyesuaikan penalaran berdasarkan persona pengguna.
  4.  **Analysis**: Mensintesis temuan menjadi jawaban yang koheren, akurat, dan sesuai dengan *Tone of Voice*.
  5.  **UI Generation**: Menyusun draft aksi (generative UI) untuk membantu pengguna mengambil langkah selanjutnya.
- **UI Implementation**:
  - `ReasoningAccordion` untuk menampilkan detail langkah orkestrasi.
  - Indikator status (Memory found, Sources found, Analysis complete) untuk setiap fase.

### 4. Agentic Continuous Learning (Memory Phase)
- **Concept**: Sistem belajar dari interaksi sebelumnya untuk meningkatkan akurasi dan efisiensi orkestrasi di masa depan.
- **Components**: `MemoryService` (Singleton) & `AgentOrchestrator`.
- **Workflow**:
  1. **Memory Retrieval**: Sebelum memulai riset baru, `AgentOrchestrator` mencari pengalaman serupa di memori melalui `MemoryService`.
  2. **Context Enrichment**: Menggunakan insight dari pengalaman sebelumnya (jika ditemukan) untuk mempercepat proses penalaran.
  3. **Experience Storage**: Setelah tugas selesai, orkestrator menyimpan hasil dan metrik performa kembali ke `MemoryService` sebagai pengalaman baru.
  4. **Self-Correction**: Mekanisme fallback otomatis jika skor evaluasi diri rendah (< 0.7) atau terdeteksi anomali.

### 5. Security & Privacy (UU PDP Compliance)
- **PII Masking**: Semua data sensitif (NIK, NPWP, Email, Nomor Telepon, Rekening Bank, Tanggal Lahir) disamarkan secara otomatis sebelum dikirim ke provider AI.
- **Data Residency**: Memastikan data sensitif tidak tersimpan secara permanen di log provider AI pihak ketiga.
- **De-masking**: Proses pengembalian data asli (unmasking) dilakukan hanya di sisi klien (device pengguna) untuk menjaga privasi.

## 📱 UI/UX States
- **Empty State**: Menampilkan saran pertanyaan populer dan riwayat pencarian terakhir.
- **Loading State**: Animasi "AI is thinking..." dengan shimmer effect dan update reasoning progress.
- **Success State**: Jawaban markdown + Source Badges + Direct Links + Follow-up input + Generative UI Draft.
- **Error State**: Graceful fallback ke pencarian statis atau FAQ populer jika layanan AI terhambat.

## ⚙️ Spesifikasi Teknis
- **Logic Services**:
  - `AgentOrchestrator.ts`: Orkestrasi multi-agen dan manajemen fase reasoning.
  - `TrustSignalService.ts`: Perhitungan skor kepercayaan, verifikasi sumber resmi, dan skor kebaruan (recency).
  - `MemoryService.ts`: Manajemen memori jangka panjang untuk pembelajaran kontinu.
- **State Management**: React Context API (Modular & Scalable).
- **UI Performance**: 
  - Memoized components pada feed chat untuk efisiensi rendering.
  - Async handling untuk operasi memori guna menghindari pemblokiran UI thread.
- **Analytics**: Event `ai_agent_performance`, `screen_view`, `conversion_event`.

## ✅ Acceptance Criteria
- [x] AI merespon dengan proses orkestrasi transparan (Reasoning Path).
- [x] Menampilkan indikator kepercayaan (Trust Signals) berbasis sumber resmi.
- [x] Implementasi memori kontinu untuk pembelajaran sistem (Memory Retrieval & Storage).
- [x] Mendukung tindak lanjut pertanyaan (*follow-up*) dalam satu sesi.
- [x] Menyertakan *disclaimer* hukum otomatis pada setiap jawaban.