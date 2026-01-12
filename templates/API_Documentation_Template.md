# API Documentation: [Nama Module/Service]

## 1. Base URL
`https://api.lawyershub.id/v1`

## 2. Endpoints

### 2.1 [GET/POST/PUT/DELETE] /[endpoint-path]
Deskripsi singkat fungsi endpoint.

**Request Headers:**
- `Authorization`: `Bearer <token>`
- `X-Tenant-Id`: `<tenant-id>`

**Parameters (Query/Body):**
| Field | Type | Required | Description |
|-------|------|----------|-------------|
| name  | string | Yes    | Deskripsi   |

**Response (200 OK):**
```json
{
  "status": "success",
  "data": { ... }
}
```

**Error Codes:**
- `400`: Bad Request
- `401`: Unauthorized
- `500`: Internal Server Error
