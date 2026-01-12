# 🔑 Auth Token Flow

1. Login via API -> Dapatkan `accessToken` & `refreshToken`.
2. Simpan di `SecureStore` (Expo).
3. Gunakan `accessToken` di header `Authorization`.
4. Refresh token otomatis saat 401.
