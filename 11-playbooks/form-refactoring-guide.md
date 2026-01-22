# 📝 Form Refactoring Guide: Zod & React Hook Form

Panduan ini menjelaskan standar baru untuk implementasi form di **ILC-APP** menggunakan integrasi **Zod** dan **React Hook Form**.

---

## 1. Tech Stack
- **React Hook Form**: Manajemen state form tanpa re-render berlebih.
- **Zod**: Validasi data yang kuat dan type-safe.
- **@hookform/resolvers/zod**: Jembatan antara React Hook Form dan Zod.

---

## 2. Struktur File Rekomendasi
Setiap fitur form harus memiliki struktur berikut:
- `ui/MyForm.tsx`: Komponen UI form.
- `model/my-form.schema.ts`: Definisi skema Zod dan tipe data.
- `ui/__tests__/MyForm.test.tsx`: Unit test untuk fungsionalitas form.

---

## 3. Contoh Implementasi

### A. Definisi Schema (`src/shared/model/search.schema.ts`)
```typescript
import { z } from 'zod';

export const simpleSearchSchema = z.object({
  query: z.string().min(1, 'Query tidak boleh kosong'),
});

export type SimpleSearchFormData = z.infer<typeof simpleSearchSchema>;
```

### B. Komponen Form (`src/features/legal-search/ui/LegalSearchBar.tsx`)
```tsx
import { useForm, Controller } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { simpleSearchSchema, SimpleSearchFormData } from '@/shared/model/search.schema';

export const LegalSearchBar = ({ onSearch, t }) => {
  const { control, handleSubmit, reset } = useForm<SimpleSearchFormData>({
    resolver: zodResolver(simpleSearchSchema),
    defaultValues: { query: '' }
  });

  const onSubmit = (data: SimpleSearchFormData) => {
    onSearch(data.query);
  };

  return (
    <View>
      <Controller
        control={control}
        name="query"
        render={({ field: { onChange, onBlur, value } }) => (
          <TextInput
            value={value}
            onChangeText={onChange}
            onBlur={onBlur}
            placeholder={t('search_placeholder')}
          />
        )}
      />
      <Button onPress={handleSubmit(onSubmit)} title={t('search')} />
    </View>
  );
};
```

### C. Penanganan Komponen Kompleks (Modal & Editor)

Untuk komponen seperti Modal atau Editor yang membutuhkan sinkronisasi state eksternal atau reset state saat modal dibuka/ditutup, gunakan `useEffect` bersama `reset` atau `setValue`.

**Contoh: EditMessageModal.tsx**
```tsx
const { control, reset, handleSubmit } = useForm<EditMessageFormData>({
  resolver: zodResolver(editMessageSchema),
  defaultValues: { text: initialText }
});

// Reset form saat modal dibuka dengan data baru
useEffect(() => {
  if (visible) {
    reset({ text: initialText });
  }
}, [visible, initialText, reset]);
```

**Contoh: CollaborativeEditor.tsx (Yjs Integration)**
Gunakan `setValue` untuk sinkronisasi state dari layanan pihak ketiga (seperti Yjs) ke dalam `react-hook-form`.

```tsx
useEffect(() => {
  if (!editor) return;

  // Sinkronisasi awal
  setValue('content', editor.getText().toString());

  // Observasi perubahan dari Yjs
  editor.observe(() => {
    const newContent = editor.getText().toString();
    setValue('content', newContent);
  });
}, [editor, setValue]);
```

---

## 4. Manfaat Refactor
1. **Performa**: Penggunaan `Controller` dan state yang tidak terpusat di root component mengurangi re-render yang tidak perlu pada setiap ketikan (keystroke).
2. **Type Safety**: Integrasi Zod memastikan data yang dikirim ke fungsi `onSubmit` selalu valid sesuai kontrak.
3. **Validasi Terpusat**: Error message dan aturan validasi didefinisikan di satu tempat (schema), memudahkan maintenance.
4. **Testability**: Form lebih mudah diuji karena menggunakan standar library yang populer dan well-supported.

---

## 5. Daftar Komponen yang Telah Direfactor (Januari 2026)
- `EditProfileScreen.tsx` (Profile Management)
- `RegisterForm.tsx` (Authentication)
- `LegalSearchBar.tsx` (Search)
- `AnnotationForm.tsx` (Document Reader)
- `FeedbackForm.tsx` (AI Feedback)
- `JustificationForm.tsx` (AI Intervention)
- `MessageList.tsx` (Chat Search)
- `ConversationList.tsx` (Inbox Search)
- `ContactList.tsx` (Contact Search)
- `aiChatContext.tsx` (History Search Query)
- `AskScreen` (Message Editing)
- `CollaborativeEditor.tsx` (Document Content & Explanation)

---
*Dibuat oleh World-Class Super Agent - 2026-01-22*
