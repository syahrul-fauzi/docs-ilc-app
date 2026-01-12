# 🤖 AI Service API Reference

Dokumen ini mendefinisikan kontrak API untuk layanan AI (Legal Engine) di ILC-APP.

## 1. Ask Legal Question
Endpoint utama untuk mengajukan pertanyaan hukum ke AI.

- **URL**: `/ai/ask`
- **Method**: `POST`
- **Auth Required**: YES (JWT Token)

### Request Body
```json
{
  "query": "Apa saja syarat PHK menurut PP 35/2021?",
  "context": {
    "location": "Jakarta",
    "previous_chat_id": "optional-id"
  }
}
```

### Success Response
- **Code**: 200 OK
- **Content**:
```json
{
  "answer": "Berdasarkan PP 35/2021, syarat PHK meliputi...",
  "confidenceScore": 0.95,
  "sources": [
    {
      "id": "ref1",
      "title": "PP No. 35 Tahun 2021",
      "content": "Pasal 36...",
      "source": "JDIH Kemenaker",
      "isVerified": true
    }
  ],
  "suggestedFollowUps": [
    "Bagaimana cara menghitung pesangon?",
    "Berapa lama proses mediasi?"
  ]
}
```

## 2. AI Reasoning Path (Internal Service)
`AgentOrchestrator` menghasilkan jalur penalaran yang dapat digunakan UI untuk menampilkan progres "berpikir" AI.

### Data Structure
```typescript
interface AgentReasoning {
  role: 'researcher' | 'analyst' | 'drafter' | 'orchestrator';
  thought: string;
  action?: string;
}
```

## 3. Trust Signals calculation
Layanan mobile melakukan validasi mandiri terhadap hasil AI menggunakan `TrustSignalService`.

### Trust Signal Schema
```typescript
interface TrustSignals {
  overallConfidence: number;      // 0.0 - 1.0
  isOfficialSource: boolean;      // Terdeteksi domain .go.id atau institusi resmi
  recencyScore: number;           // Skor kemutakhiran data (fokus regulasi post-2021)
  verificationStatus: 'verified' | 'partially_verified' | 'unverified';
}
```

## 4. Performance Benchmarks
- **Target Latency**: < 3000ms (p95)
- **Minimum Confidence**: 0.70
- **Official Source Priority**: Hasil dari JDIH, BPN, dan Mahkamah Agung diutamakan.
