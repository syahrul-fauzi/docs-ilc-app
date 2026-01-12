# � Billing Module API Contract

Dokumen ini mendefinisikan kontrak API untuk modul Billing di ILC-APP.

## Base URL
`${CONFIG.API_URL}/billing`

## Endpoints

### 1. Get Subscription Tiers
Mengambil daftar paket langganan yang tersedia.

- **URL**: `/tiers`
- **Method**: `GET`
- **Auth Required**: No
- **Response**: `SubscriptionTier[]`
  ```json
  [
    {
      "id": "free",
      "name": "Free",
      "price": 0,
      "currency": "IDR",
      "features": ["Feature A", "Feature B"],
      "isPopular": false
    },
    ...
  ]
  ```

### 2. Get Billing History
Mengambil riwayat transaksi pengguna.

- **URL**: `/history`
- **Method**: `GET`
- **Auth Required**: Yes (JWT)
- **Response**: `BillingHistory[]`
  ```json
  [
    {
      "id": "inv_123",
      "date": "2026-01-10T08:00:00Z",
      "amount": 99000,
      "currency": "IDR",
      "status": "success",
      "tierName": "Premium"
    }
  ]
  ```

### 3. Subscribe to Tier
Melakukan pendaftaran paket langganan.

- **URL**: `/subscribe`
- **Method**: `POST`
- **Auth Required**: Yes (JWT)
- **Request Body**:
  ```json
  {
    "tierId": "string",
    "promoCode": "string (optional)"
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "subscriptionId": "sub_987"
  }
  ```

### 4. Get Dynamic Price
Menghitung harga dinamis untuk konsultasi berdasarkan pengacara dan durasi.

- **URL**: `/price/:lawyerId`
- **Method**: `GET`
- **Query Params**: `duration` (integer, minutes)
- **Auth Required**: Yes (JWT)
- **Response**:
  ```json
  {
    "price": 250000,
    "currency": "IDR"
  }
  ```

## Error Handling
Semua endpoint mengikuti format error standar:
```json
{
  "error": {
    "code": "BILLING_ERROR",
    "message": "Deskripsi kesalahan dalam bahasa Indonesia",
    "details": {}
  }
}
```

## Security
- Semua request yang membutuhkan Auth wajib menyertakan `Authorization: Bearer <JWT_TOKEN>`.
- Header `X-Tenant-ID` wajib dikirimkan untuk identifikasi aplikasi.
