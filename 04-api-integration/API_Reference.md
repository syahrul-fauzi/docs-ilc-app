# 🔌 API Reference - ILC-APP

Dokumen ini berisi spesifikasi kontrak API dan contoh payload untuk integrasi layanan di ILC-APP.

---

## 1. AI Legal Engine

### `POST /ask`
Digunakan untuk mengajukan pertanyaan hukum ke AI Legal Engine.

**Request Body:**
```json
{
  "query": "Apa syarat sahnya perjanjian menurut KUHPerdata?",
  "context": {
    "location": "Jakarta",
    "topic": "Hukum Perdata"
  }
}
```

**Response:**
```json
{
  "answerText": "Syarat sahnya perjanjian menurut Pasal 1320 KUHPerdata adalah: 1. Kesepakatan mereka yang mengikatkan dirinya; 2. Kecakapan untuk membuat suatu perikatan; 3. Suatu pokok persoalan tertentu; 4. Suatu sebab yang tidak terlarang.",
  "sources": [
    {
      "title": "KUHPerdata Pasal 1320",
      "url": "https://jdih.mahkamahagung.go.id/peraturan/kuhperdata",
      "confidence": 0.98
    }
  ],
  "confidenceScore": 0.95,
  "trustSignals": ["Verified Source", "Official Regulation"]
}
```

---

## 2. Legal Consultations

### `GET /consultations`
Mengambil daftar riwayat konsultasi pengguna.

**Response Example:**
```json
[
  {
    "id": "cons-123",
    "lawyerName": "Dr. Hotman Paris, S.H., M.Hum.",
    "status": "completed",
    "date": "2026-01-10T10:00:00Z",
    "topic": "Sengketa Properti",
    "lastMessage": "Terima kasih atas sarannya, Dok."
  },
  {
    "id": "cons-124",
    "lawyerName": "Luhut Binsar, S.H.",
    "status": "ongoing",
    "date": "2026-01-11T14:30:00Z",
    "topic": "Investasi Asing"
  }
]
```

---

## 3. Notifications

### `GET /notifications`
Mengambil notifikasi terbaru untuk pengguna.

**Response Example:**
```json
{
  "unreadCount": 2,
  "notifications": [
    {
      "id": "notif-001",
      "type": "CONSULTATION_UPDATE",
      "title": "Jadwal Konsultasi",
      "message": "Pengacara Anda telah mengonfirmasi jadwal besok pukul 10:00.",
      "timestamp": "2026-01-11T08:00:00Z",
      "isRead": false
    },
    {
      "id": "notif-002",
      "type": "COMMUNITY_ENGAGEMENT",
      "title": "Postingan Baru",
      "message": "Seseorang mengomentari diskusi Anda tentang UU Cipta Kerja.",
      "timestamp": "2026-01-11T07:45:00Z",
      "isRead": false
    }
  ]
}
```

---

## 4. Authentication

### `POST /auth/login`
Melakukan autentikasi pengguna.

**Request Body:**
```json
{
  "email": "user@lawyershub.id",
  "password": "securepassword123"
}
```

**Response Example:**
```json
{
  "status": "success",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
  "user": {
    "id": "user-999",
    "name": "Budi Santoso",
    "role": "PRO_LAWYER",
    "email": "user@lawyershub.id"
  },
  "expiresIn": 3600
}
```

---

## 5. Error Codes

| Code | Description | Action |
|------|-------------|--------|
| 400 | Bad Request | Periksa parameter input |
| 401 | Unauthorized | Refresh token atau login kembali |
| 403 | Forbidden | Akses ditolak (cek role) |
| 404 | Not Found | Resource tidak ditemukan |
| 500 | Server Error | Hubungi tim DevOps |

---
*Last Updated: 2026-01-11*
