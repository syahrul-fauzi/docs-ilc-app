# 🎨 ILC-APP Design System & NativeWind v4 Standardization

Dokumen ini menjelaskan standar desain, penggunaan tema, dan panduan aksesibilitas untuk proyek **ILC-APP** menggunakan **NativeWind v4**.

---

## 1. Arsitektur Tema

Aplikasi menggunakan sistem variabel CSS yang terintegrasi antara `global.css` dan `tailwind.config.js`. Ini memungkinkan transisi tema (light/dark) yang mulus dan konsisten.

### 1.1 Variabel Inti
Gunakan utility classes berikut untuk memastikan konsistensi warna:

| Element | Utility Class | Description |
|---------|---------------|-------------|
| Background | `bg-background` | Warna latar belakang utama layar. |
| Foreground | `text-foreground` | Warna teks utama. |
| Card | `bg-card` | Warna latar belakang kartu/komponen kontainer. |
| Primary | `bg-primary`, `text-primary` | Warna identitas brand (Deep Blue). |
| Muted | `bg-muted`, `text-muted-foreground` | Warna untuk elemen sekunder/non-prioritas. |
| Border | `border-border` | Warna garis tepi standar. |

### 1.2 Penggunaan Warna Dinamis
Hindari penggunaan hex code langsung di komponen. Gunakan `hsl(var(--variable))` jika perlu memberikan warna pada prop komponen (seperti `IconSymbol`). 

**PENTING**: Larangan penggunaan hex code juga berlaku untuk file konstanta `.ts` (misal: `colors.ts`). Gunakan nilai HSL yang sesuai dengan tema.

Contoh:
```tsx
<IconSymbol name="info" color="hsl(var(--primary))" />
```

---

## 2. Standar Aksesibilitas (WCAG 2.1 AA)

Semua komponen wajib memenuhi standar aksesibilitas berikut:

### 2.1 Kontras Warna
- Teks normal minimal **4.5:1**.
- Elemen grafis/ikon minimal **3:1**.
- Semua variabel di `global.css` telah divalidasi untuk memenuhi standar ini pada mode terang dan gelap.

### 2.2 Atribut Aksesibilitas
Wajib menyertakan atribut berikut pada elemen interaktif:
- `accessible={true}`: Menandai elemen sebagai elemen aksesibilitas tunggal.
- `accessibilityLabel`: Deskripsi tekstual untuk screen reader (Gunakan Bahasa Indonesia).
- `accessibilityRole`: Peran elemen (misal: `button`, `header`, `summary`, `image`).
- `accessibilityState`: Status elemen (misal: `{ expanded: true }`, `{ disabled: true }`).

**Catatan**: Komponen atomik (`Button`, `Input`, `CardTitle`) sudah memiliki peran aksesibilitas default. Selalu berikan `accessibilityLabel` yang deskriptif saat menggunakan komponen ini.

---

## 3. Komponen UI Utama

### 3.1 Button
Komponen tombol serbaguna dengan dukungan feedback visual (Ripple di Android, Opacity di iOS).

**Props:**
- `variant`: `'default' | 'destructive' | 'outline' | 'secondary' | 'ghost' | 'link'`
- `size`: `'default' | 'sm' | 'lg' | 'icon'`
- `textClass`: String untuk styling tambahan pada teks di dalam tombol.
- `...PressableProps`: Mendukung semua props dari React Native `Pressable`.

**Contoh:**
```tsx
<Button variant="primary" onPress={() => console.log("Pressed")}>
  <Text>Mulai Konsultasi</Text>
</Button>
```

### 3.2 Input
Input teks yang konsisten dengan dukungan accessibility state dan styling error.

**Props:**
- `...TextInputProps`: Mendukung semua props dari React Native `TextInput`.
- `className`: Untuk kustomisasi container.

**Contoh:**
```tsx
<Input 
  placeholder="Tulis pesan Anda..." 
  value={message} 
  onChangeText={setMessage}
  accessibilityLabel="Input pesan hukum"
/>
```

### 3.3 Checkbox
Elemen seleksi tunggal dengan state yang dapat dikontrol.

**Props:**
- `checked`: Boolean status centang.
- `onCheckedChange`: Callback saat status berubah.
- `disabled`: Boolean untuk menonaktifkan interaksi.

**Contoh:**
```tsx
<Checkbox 
  checked={agreed} 
  onCheckedChange={setAgreed}
  accessibilityLabel="Setujui syarat dan ketentuan"
/>
```

### 3.4 Badge
Indikator status atau label kecil.

**Props:**
- `variant`: `'default' | 'secondary' | 'destructive' | 'outline'`

**Contoh:**
```tsx
<Badge variant="secondary">
  <Text>Terverifikasi</Text>
</Badge>
```

### 3.5 Card
Komponen kontainer untuk mengelompokkan informasi terkait.

**Sub-komponen:**
- `Card`: Kontainer utama.
- `CardHeader`: Bagian atas kartu (padding & spacing).
- `CardTitle`: Judul kartu (ukuran teks h3).
- `CardDescription`: Deskripsi kartu (teks muted).
- `CardContent`: Konten utama kartu.
- `CardFooter`: Bagian bawah kartu (biasanya untuk aksi).

**Contoh:**
```tsx
<Card>
  <CardHeader>
    <CardTitle><Text>Detail Kasus</Text></CardTitle>
    <CardDescription><Text>Nomor Perkara: 123/Pdt.G/2025</Text></CardDescription>
  </CardHeader>
  <CardContent>
    <Text>Konten detail kasus di sini...</Text>
  </CardContent>
  <CardFooter>
    <Button><Text>Lihat Selengkapnya</Text></Button>
  </CardFooter>
</Card>
```

### 3.6 Switch
Komponen toggle biner untuk pengaturan.

**Props:**
- `checked`: Boolean status aktif.
- `onCheckedChange`: Callback saat status berubah.
- `disabled`: Menonaktifkan interaksi.

**Contoh:**
```tsx
<Switch 
  checked={notifications} 
  onCheckedChange={setNotifications}
  accessibilityLabel="Aktifkan notifikasi"
/>
```

### 3.7 Spinner
Indikator pemuatan (loading) yang konsisten.

**Props:**
- `size`: `'small' | 'large'`
- `color`: Warna spinner (opsional, default: primary).

**Contoh:**
```tsx
<Spinner size="large" accessibilityLabel="Sedang memproses data" />
```

### 3.8 IconSymbol
Komponen ikon lintas platform (SF Symbols di iOS, Material Icons di Android).

**Props:**
- `name`: Nama ikon (berdasarkan SF Symbols mapping).
- `size`: Ukuran ikon (default: 20).
- `color`: Warna ikon (WAJIB menggunakan `hsl(var(--variable))`).

**Contoh:**
```tsx
<IconSymbol name="house.fill" color="hsl(var(--primary))" />
```

### 3.9 Typography (Text)
Sistem tipografi yang konsisten.

**Variants:**
- `h1` s/d `h6`: Heading styles.
- `p`: Paragraph style (default).
- `lead`: Teks pembuka yang lebih besar.
- `muted`: Teks sekunder (warna abu-abu).
- `small`: Teks keterangan kecil.

**Contoh:**
```tsx
<Text variant="h1">Judul Utama</Text>
<Text variant="muted">Keterangan tambahan di sini.</Text>
```

### 3.10 ReasoningAccordion
Komponen khusus untuk menampilkan langkah-langkah penalaran AI secara transparan.

**Props:**
- `path`: Array objek penalaran AI (role, thought, action).

**Contoh:**
```tsx
<ReasoningAccordion path={aiThoughtProcess} />
```

### 3.11 Dialog (Modal)
Komponen dialog overlay untuk interaksi terfokus.

**Sub-komponen:**
- `Dialog`: Provider konteks.
- `DialogTrigger`: Elemen pemicu (biasanya tombol).
- `DialogContent`: Kontainer konten modal (termasuk overlay).
- `DialogHeader`: Bagian atas dialog (judul & deskripsi).
- `DialogFooter`: Bagian bawah dialog (aksi).

**Contoh:**
```tsx
<Dialog open={showModal} onOpenChange={setShowModal}>
  <DialogTrigger asChild>
    <Button><Text>Buka Dialog</Text></Button>
  </DialogTrigger>
  <DialogContent>
    <DialogHeader>
      <DialogTitle><Text>Konfirmasi</Text></DialogTitle>
      <DialogDescription><Text>Apakah Anda yakin ingin melanjutkan?</Text></DialogDescription>
    </DialogHeader>
    <DialogFooter>
      <Button variant="outline" onPress={() => setShowModal(false)}><Text>Batal</Text></Button>
      <Button onPress={handleConfirm}><Text>Lanjut</Text></Button>
    </DialogFooter>
  </DialogContent>
</Dialog>
```

### 3.12 DataTable
Komponen tabel data yang komprehensif dengan fitur pengurutan, paginasi, dan seleksi.

**Props Utama:**
- `rows`: Array data objek.
- `columns`: Definisi kolom (`field`, `headerName`, `width`, `renderCell`).
- `loading`: Menampilkan state pemuatan.
- `selectable`: Aktifkan checkbox seleksi baris.
- `page` & `pageSize`: Kontrol paginasi.

**Contoh:**
```tsx
<DataTable 
  rows={lawyers} 
  columns={[
    { field: 'name', headerName: 'Nama', flex: 1 },
    { field: 'specialization', headerName: 'Spesialisasi', width: 150 },
    { field: 'rating', headerName: 'Rating', width: 80, align: 'center' }
  ]}
/>
```

---

## 4. Panduan Pengembangan & Best Practices

1. **Gunakan Utility Classes**: Prioritaskan NativeWind classes daripada `StyleSheet` untuk kemudahan pemeliharaan dan dukungan tema.
2. **Dark Mode Ready**: Pastikan setiap komponen diuji pada kedua mode. Variabel CSS di `global.css` menangani sebagian besar kasus secara otomatis.
3. **No Hardcoded Hex**: Dilarang keras menggunakan hex code (`#FFFFFF`) di dalam file `.tsx` dan `.ts`. Gunakan variabel tema `hsl(var(--variable))` atau konstanta dari `tailwind.config.js`.
4. **Aksesibilitas adalah Prioritas**: Setiap komponen interaktif WAJIB memiliki `accessibilityLabel` dan `accessibilityRole`.
5. **Responsive Spacing**: Gunakan sistem spacing Tailwind (`p-4`, `m-2`, `gap-4`) untuk menjaga konsistensi layout.

---

## 5. Dokumentasi Versi & Perubahan

| Versi | Tanggal | Deskripsi Perubahan |
|-------|---------|---------------------|
| v1.0.0 | 2026-01-11 | Inisialisasi sistem desain dengan NativeWind v4. |
| v1.1.0 | 2026-01-12 | Audit aksesibilitas WCAG 2.1 AA dan standarisasi variabel warna. |
| v1.2.0 | 2026-01-12 | Penambahan dokumentasi komponen utama (Button, Input, Checkbox, Badge). |
