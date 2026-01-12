# Feature Specification Template: {{feature_name}}

## 1. Objective
Jelaskan tujuan utama dari fitur ini dan masalah apa yang ingin diselesaikan.

## 2. User Stories
- Sebagai {{role}}, saya ingin {{need}} sehingga {{benefit}}.
- Sebagai {{role}}, saya ingin {{need}} sehingga {{benefit}}.

## 3. Acceptance Criteria
- [ ] Kriteria 1: Deskripsi detail.
- [ ] Kriteria 2: Deskripsi detail.
- [ ] Kriteria 3: Deskripsi detail.

## 4. Technical Design
### 4.1 UI/UX
- Referensi desain: [Link Figma/Screenshot]
- Komponen baru yang dibutuhkan:
  - `ComponentNameA`
  - `ComponentNameB`

### 4.2 Domain Logic
- Model data: `{{EntityName}}`
- Logic khusus: Penjelasan algoritma atau aturan bisnis.

### 4.3 API Contract
**Endpoint**: `POST /api/{{feature-name}}`
**Request**:
```json
{
  "param1": "value"
}
```
**Response**:
```json
{
  "status": "success",
  "data": {}
}
```

## 5. Testing Plan
- Unit test untuk logic `X`.
- Integration test untuk flow `Y`.
- Manual test untuk UI `Z`.

---
*Status: Draft / In Review / Approved*
