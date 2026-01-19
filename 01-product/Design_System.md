# ILC-APP Design System
## Branding & UI Tokens

Dokumen ini mendefinisikan standar visual dan komponen UI untuk **ILC-APP**, memastikan konsistensi di seluruh platform mobile.

---

## 🎨 Color Palette (Tokens)

Warna-warna ini didefinisikan dalam `global.css` dan `constants/Colors.ts`.

### 1. Primary Colors
| Token | Hex (Light) | Hex (Dark) | Name | Usage |
| :--- | :--- | :--- | :--- | :--- |
| `primary` | `#1E3A8A` | `#60A5FA` | Blue | Brand identity, buttons, active states. |
| `primary-foreground` | `#F8FAFC` | `#030712` | Slate 50/950 | Text on primary backgrounds. |

### 2. Accent Colors
| Token | Hex (Light) | Hex (Dark) | Name | Usage |
| :--- | :--- | :--- | :--- | :--- |
| `accent` | `#059669` | `#12D38A` | Emerald Green | Trust indicators, success states, highlights. |
| `accent-foreground` | `#FFFFFF` | `#030712` | Dark Slate | Text on accent backgrounds (WCAG 2.1). |

### 3. Feedback Colors (WCAG 2.1 Compliant)
| Token | Hex (Light) | Hex (Dark) | Name | Usage |
| :--- | :--- | :--- | :--- | :--- |
| `success` | `#16A34A` | `#3BE87E` | Emerald/Green | Success messages, positive indicators. |
| `success-foreground` | `#FFFFFF` | `#003308` | Dark Green | Text on success backgrounds. |
| `warning` | `#F59E0B` | `#F9D639` | Amber/Yellow | Warning alerts, caution indicators. |
| `warning-foreground` | `#311F03` | `#311F03` | Dark Brown | Text on warning backgrounds. |
| `destructive` | `#DC2626` | `#F33F3F` | Red | Errors, destructive actions, alerts. |
| `destructive-foreground` | `#FFFFFF` | `#030712` | Dark Slate | Text on destructive backgrounds. |

### 3. Neutral Colors
| Token | Hex | Name | Usage |
| :--- | :--- | :--- | :--- |
| `background` | `#FFFFFF` | White | Main screen backgrounds. |
| `foreground` | `#0F172A` | Slate 900 | Main body text. |
| `muted` | `#F1F5F9` | Slate 100 | Background for inactive elements/cards. |
| `border` | `#E2E8F0` | Slate 200 | Dividers and element borders. |

---

## typography Skala Tipografi

Menggunakan font **Sans Serif Human-friendly** (System Default atau Inter).

| Level | Size | Weight | Line Height | Usage |
| :--- | :--- | :--- | :--- | :--- |
| **H1** | 24px | Bold | 32px | Screen Titles |
| **H2** | 20px | SemiBold | 28px | Section Headers |
| **Body** | 16px | Regular | 24px | Main Content |
| **Small** | 14px | Medium | 20px | Captions, Metadata |

---

## 🧱 Component Standards

### 1. Buttons
- **Primary:** `bg-primary text-primary-foreground`. Digunakan untuk aksi utama (e.g., "Tanya Sekarang").
- **Secondary:** `bg-secondary text-secondary-foreground`. Untuk aksi pendukung.
- **Outline:** `border border-input`. Untuk aksi tersier.

### 2. Chat Bubbles
- **User Message:** `bg-primary text-primary-foreground`. Alignment: Right.
- **Lawyer/AI Message:** `bg-muted text-foreground`. Alignment: Left.
- **Timestamp:** `text-small text-muted-foreground`.

### 3. Headers
- **Background:** `bg-background` atau `bg-primary` (untuk profil/brand focus).
- **Text:** `text-foreground` atau `text-primary-foreground`.
- **Icons:** Menggunakan `IconSymbol` dengan warna `tint`.

### 4. Trust Signals (Ultra-Minimalist Approach)
- **Container:** `flex-row justify-center items-center gap-8 mt-12 w-full py-2`.
- **Dividers:** Circular dot dividers using `w-1 h-1 rounded-full bg-border/40`.
- **Typography:** `text-[10px] font-bold text-muted-foreground uppercase tracking-[1.5px]`.
- **Iconography:** `IconSymbol` with `size={12}` and monochromatic `muted-foreground` color.
- **Goal:** Memberikan jaminan keamanan dan kecepatan secara subliminal tanpa mengganggu fokus utama pada area kueri.

---

## 🛠️ Implementation Guide

### Tailwind Classes
Gunakan utilitas Tailwind untuk menerapkan desain secara cepat:
```tsx
// Contoh Button
<Button className="bg-primary px-4 py-2">
  <Text className="text-primary-foreground font-bold">Tanya Hukum</Text>
</Button>

// Contoh Card
<Card className="border-border bg-card p-4">
  <Text className="text-foreground">Konten hukum di sini...</Text>
</Card>
```

### Dark Mode
Pastikan menggunakan prefix `dark:` untuk dukungan tema gelap:
```css
.dark {
  --background: 224 71.4% 4.1%;
  --primary: 224 64% 45%;
}
```
