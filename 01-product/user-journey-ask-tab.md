# User Journey Map: Tab "Ask" (AI Consultation)

## 1. Overview
User Journey ini mendokumentasikan langkah-langkah, emosi, dan hambatan yang dialami pengguna saat berinteraksi dengan fitur konsultasi hukum berbasis AI di ILC-APP.

## 2. Persona Utama: Andi (Masyarakat Umum)
- **Profil**: Pria, 35 tahun, sedang menghadapi masalah sengketa waris.
- **Goal**: Mendapatkan kepastian hukum awal secara cepat dan gratis sebelum memutuskan menyewa pengacara.

## 3. Journey Map

| Tahap | Aktivitas Pengguna | Pikiran & Perasaan | Pain Points (Hambatan) | Peluang UX & Solusi |
| :--- | :--- | :--- | :--- | :--- |
| **1. Entry** | Membuka tab "Ask" dari menu navigasi utama. | "Saya harap AI ini bisa membantu masalah warisan saya." | Bingung harus mulai dari mana jika layar kosong. | **AskQuickTips**: Memberikan saran pertanyaan awal (Contextual Onboarding). |
| **2. Discovery** | Melihat saran pertanyaan dan filter "Case Type". | "Oh, ada kategori Perdata, mungkin saya klik itu dulu." | Istilah hukum yang terlalu teknis di filter. | **Case Type Chips**: Menggunakan bahasa yang lebih manusiawi (Fixed). |
| **3. Formulation** | Mulai mengetik pertanyaan tentang "sengketa tanah warisan". | "Bagaimana cara menjelaskan kasus saya dengan benar?" | Capek mengetik detail yang panjang. | **Smart Suggestions & Voice Input**: Mempercepat proses input (Fixed). |
| **4. Processing** | Menunggu AI memproses jawaban (Thinking Agent). | "Apa yang sedang dilakukan AI? Kenapa lama sekali?" | Kecemasan saat menunggu tanpa feedback visual. | **ThinkingAgent Visuals**: Menampilkan status "Researching laws..." secara real-time (Fixed). |
| **5. Review** | Membaca jawaban AI dan mengecek sumber hukum. | "Apakah jawaban ini bisa dipercaya? Mana dasar hukumnya?" | Teks jawaban yang terlalu padat dan kaku. | **Trust Signals & Citations**: Badge verifikasi dan link langsung ke JDIH (Fixed). |
| **6. Evaluation** | Menilai kualitas jawaban (Like/Dislike) atau lapor error. | "Jawaban ini bagus, tapi saya ingin melaporkan sedikit kesalahan." | Form laporan yang rumit dan panjang. | **UAT Feedback Modal**: Form minimalis dengan pilihan kategori cepat (Fixed). |
| **7. Exit/Next** | Menyimpan jawaban atau lanjut ke konsultasi pengacara. | "Saya rasa saya butuh pengacara profesional sekarang." | Putus alur (dead end) setelah mendapatkan jawaban AI. | **Conversion Loop**: Tombol "Cari Pengacara" di akhir jawaban AI. |

## 4. Key UX Principles Applied
- **Progressive Disclosure**: Menyembunyikan opsi tuning yang kompleks di dalam modal.
- **Immediate Feedback**: Memberikan indikasi visual saat merekam suara atau AI sedang berpikir.
- **Accessibility First**: Memastikan semua teks terbaca oleh pengguna dengan berbagai kondisi penglihatan.

---
*Update Terakhir: 18 Januari 2026*
