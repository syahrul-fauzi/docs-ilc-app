# Quality Assurance Strategy — ILC-APP

Strategi ini memastikan setiap rilis ILC-APP memenuhi standar kualitas tinggi, reliabilitas, dan keamanan.

## 1. Testing Pyramid
Kami menerapkan tiga lapisan pengujian untuk efisiensi dan cakupan maksimal:

### 1.1 Unit Testing (Dasar)
- **Target**: Fungsi utilitas, domain logic, dan custom hooks.
- **Tool**: Jest.
- **Goal**: Menjamin setiap fungsi kecil berjalan sesuai ekspektasi secara terisolasi.

### 1.2 Integration Testing (Menengah)
- **Target**: Interaksi antar komponen UI dan API Services.
- **Tool**: React Testing Library + MSW (Mock Service Worker).
- **Goal**: Menjamin flow data antara UI dan Backend berjalan lancar.

### 1.3 End-to-End (E2E) Testing (Puncak)
- **Target**: Critical User Journeys (Login -> Ask -> Consult).
- **Tool**: Detox (Mobile) / Playwright (Web).
- **Goal**: Simulasi perilaku pengguna nyata pada sistem yang sudah terintegrasi.

---

## 2. Metrik Kualitas Kode
Setiap Pull Request harus memenuhi ambang batas berikut sebelum di-merge:

| Metrik | Ambang Batas (Threshold) | Alat Ukur |
|--------|--------------------------|-----------|
| Code Coverage | ≥ 80% | Jest Coverage |
| Lint Errors | 0 | ESLint |
| Type Errors | 0 | TypeScript Compiler |
| Build Success | 100% | CI Pipeline |
| Performance (FCP) | < 1.5 detik | Lighthouse / Firebase Perf |

---

## 3. Prosedur Code Review
Setiap perubahan kode wajib ditinjau oleh minimal satu peer reviewer dengan fokus pada:
- **Clean Code**: Keterbacaan dan kesederhanaan.
- **Security**: Tidak ada hardcoded secrets atau celah XSS.
- **Architecture**: Kepatuhan terhadap pola FSD/DDD.
- **Consistency**: Penggunaan tema warna dan komponen UI standar.

---

## 4. Continuous Integration (CI)
Setiap Pull Request akan memicu pipeline otomatis:
1. `npm install`
2. `npm run lint`
3. `npm run type-check`
4. `npm test`
- PR hanya bisa di-merge jika semua tahap di atas sukses.

---
*Ditetapkan oleh Tim QA ILC-APP - Januari 2026*
