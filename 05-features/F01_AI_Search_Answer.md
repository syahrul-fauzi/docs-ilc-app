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

### 3. Reasoning Transparency (The "2 Logs" Component)
- **Concept**: Menampilkan proses berpikir AI secara transparan untuk meningkatkan kepercayaan pengguna.
- **Component**: `ReasoningAccordion`
- **Flow**:
  1.  **Orchestrator**: Menganalisis intent pengguna dan merencanakan strategi pencarian.
  2.  **Researcher**: Melakukan pencarian mendalam pada database hukum (UU, Putusan, Artikel).
  3.  **Analyst**: Mensintesis temuan menjadi jawaban yang koheren dan actionable.
- **UI Implementation**:
  - Accordion yang dapat dibuka/tutup untuk melihat detail setiap langkah.
  - Indikator status (Loading, Completed, Error) untuk setiap langkah.
  - Penggunaan warna dan ikon yang intuitif untuk membedakan peran (Orchestrator, Researcher, Analyst).

### 4. Agentic Continuous Learning (Memory Phase)
- **Concept**: Sistem belajar dari interaksi sebelumnya untuk meningkatkan akurasi dan efisiensi orkestrasi di masa depan.
- **Components**: `MemoryService` & `AgentOrchestrator`.
- **Workflow**:
  1. **Memory Retrieval**: Sebelum memulai riset baru, Orchestrator mencari pengalaman serupa di memori (MMKV/SecureStore).
  2. **Context Enrichment**: Jika ditemukan, Orchestrator menggunakan insight dari pengalaman sebelumnya untuk mempercepat analisis.
  3. **Feedback Loop**: Setelah tugas selesai, pengguna dapat memberikan feedback (rating 1-5). Feedback ini disimpan kembali ke memori untuk koreksi di masa depan.
  4. **Self-Correction**: Jika skor kepercayaan rendah (< threshold), sistem akan secara otomatis menambahkan label peringatan dan mencoba strategi alternatif.

## 📱 UI/UX States
- **Empty State**: Menampilkan saran pertanyaan populer dan riwayat pencarian terakhir (cached).
- **Loading State**: Animasi "AI is thinking..." dengan shimmer effect.
- **Success State**: Jawaban markdown + Source Badges + Direct Links + Follow-up input.
- **Error State**: Graceful fallback ke pencarian statis atau FAQ populer jika layanan AI terhambat.

## ⚙️ Spesifikasi Teknis
- **Endpoint**: `POST /v1/ai/ask`
- **Logic Service**: `services/ai.ts` (Implementasi `calculateTrustSignals`).
- **State Management**: React Context (`CopilotContext.tsx`) & Recoil (history & context).
- **UI Performance**: 
  - Memoized `MessageBubble` & `TrustBadge` untuk efisiensi rendering.
  - `useCallback` pada handler pencarian untuk stabilitas referensi.
- **Caching**: Local caching (SQLite/MMKV) untuk pencarian berulang.
- **Analytics**: Event `ai_search_query`, `ai_answer_shared_to_community`.

## ✅ Acceptance Criteria
- [ ] AI merespon dalam waktu < 3 detik (Target SLO).
- [ ] Menampilkan referensi hukum dengan tautan langsung ke pasal terkait.
- [ ] Mendukung tindak lanjut pertanyaan (*follow-up*) dalam satu sesi.
- [ ] Menyertakan *disclaimer* hukum otomatis pada setiap jawaban.