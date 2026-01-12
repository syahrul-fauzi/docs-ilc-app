# ⚖️ F02: Consultation Workflow & Monetization

## 📝 Deskripsi
Alur untuk menghubungkan pengguna dengan pengacara mitra setelah mendapatkan jawaban awal dari AI, serta pengelolaan transaksi dan model pendapatan platform.

## 🔄 Workflow Step
1. **Trigger**: Klik tombol "Konsultasi Lanjut" di hasil pencarian AI.
2. **Dynamic Matching**: 
   - User mengisi detail kasus.
   - Sistem menampilkan daftar pengacara dengan **Dynamic Pricing** (berdasarkan senioritas, rating, dan urgensi).
3. **Selection & Payment**:
   - User memilih pengacara dan jadwal.
   - Integrasi **In-App Payment Flow** (GoPay, OVO, Bank Transfer).
4. **Consultation**: Sesi dimulai via Chat/Call/Video Call.

## 💰 Strategi Monetisasi
### 1. Subscription Models (Freemium)
- **Free Tier**: 3x AI Search/hari, akses feed komunitas terbatas.
- **Premium Tier**: Unlimited AI Search, diskon biaya konsultasi 10%, akses prioritas ke pengacara senior.
- **Lawyer/Firm Tier**: Dashboard manajemen kasus, analytics, dan lead generation.

### 2. Transactional Revenue
- Biaya administrasi per sesi konsultasi sukses.
- Biaya layanan untuk fitur *Document Automation*.

## ✅ Acceptance Criteria
- [ ] Integrasi payment gateway berhasil memproses transaksi dalam < 30 detik.
- [ ] Notifikasi dikirim ke pengacara dalam < 1 menit via Push Notification.
- [ ] Status langganan (Free/Premium) tersinkronisasi di seluruh aplikasi secara real-time.
- [ ] Transparansi biaya: User harus melihat rincian biaya sebelum konfirmasi pembayaran.