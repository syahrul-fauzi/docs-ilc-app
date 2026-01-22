# Panduan Refactor Form: Zod & React Hook Form

Dokumen ini mendokumentasikan standar baru implementasi form di ILC-APP menggunakan kombinasi **React Hook Form** dan **Zod**.

## 1. Latar Belakang

Sebelumnya, manajemen state form menggunakan `useState` yang menyebabkan:
- Re-render berlebihan pada setiap ketikan (keystroke).
- Validasi manual yang tersebar dan repetitif.
- Kesulitan dalam testing logika validasi.
- Tipe data yang tidak konsisten antara UI dan API.

Solusi baru mengadopsi **React Hook Form (RHF)** untuk manajemen state yang performan (uncontrolled components) dan **Zod** untuk skema validasi yang terpusat dan type-safe.

## 2. Arsitektur & Pola Implementasi

### 2.1 Struktur File
Setiap fitur yang memiliki form kompleks wajib mengikuti struktur:
```
features/<feature>/
├── model/
│   ├── <feature>.schema.ts    # Skema Zod & Type Inference
│   └── ...
├── ui/
│   ├── <Feature>Form.tsx      # Komponen Form
│   └── ...
```

### 2.2 Definisi Skema (Schema Definition)
Gunakan `z.object` untuk mendefinisikan bentuk data dan pesan error.
**Contoh (`src/shared/model/search.schema.ts`):**
```typescript
import { z } from 'zod';

export const simpleSearchSchema = z.object({
  query: z.string().min(1, 'Pencarian tidak boleh kosong'),
});

export type SimpleSearchFormData = z.infer<typeof simpleSearchSchema>;
```

### 2.3 Implementasi Komponen (Component Implementation)
Gunakan hook `useForm` dengan `zodResolver`.
**Contoh:**
```typescript
import { useForm, Controller } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { simpleSearchSchema, SimpleSearchFormData } from '../model/search.schema';

export const SearchComponent = () => {
  const { control, handleSubmit } = useForm<SimpleSearchFormData>({
    resolver: zodResolver(simpleSearchSchema),
    defaultValues: { query: '' }
  });

  const onSubmit = (data: SimpleSearchFormData) => {
    // data terjamin valid dan sesuai tipe
    console.log(data.query);
  };

  return (
    <Controller
      control={control}
      name="query"
      render={({ field: { onChange, value }, fieldState: { error } }) => (
        <>
          <TextInput 
            value={value} 
            onChangeText={onChange} 
            // ... styling
          />
          {error && <Text>{error.message}</Text>}
        </>
      )}
    />
  );
};
```

## 3. Komponen yang Telah Direfactor

Berikut adalah daftar komponen prioritas yang telah dimigrasi:

| Komponen | Lokasi | Skema | Status |
|----------|--------|-------|--------|
| **AskInputZone** | `features/ai-chat/ui/AskInputZone.tsx` | `askInputSchema` | ✅ Selesai |
| **EditMessageModal** | `features/ai-chat/ui/EditMessageModal.tsx` | `editMessageSchema` | ✅ Selesai |
| **CollaborativeEditor** | `features/document-editor/ui/CollaborativeEditor.tsx` | `editorSchema` | ✅ Selesai |
| **RegisterForm** | `features/auth/ui/RegisterForm.tsx` | `registerSchema` | ✅ Selesai |
| **ConsultationForm** | `features/consultation/ui/ConsultationFormDialog.tsx` | `consultationSchema` | ✅ Selesai |
| **CommunityFeed** | `features/community/ui/CommunityFeed.tsx` | `postSchema` | ✅ Selesai |
| **SplitViewReader** | `features/ai-chat/ui/SplitViewReader.tsx` | `annotationSchema` | ✅ Selesai |
| **MessageList** | `features/personal-chat/ui/MessageList.tsx` | `simpleSearchSchema` | ✅ Selesai |

## 4. Panduan Testing

Untuk unit test komponen yang menggunakan RHF, gunakan pola mock berikut di Jest:

```typescript
// Mock komponen form jika diperlukan
jest.mock('@/path/to/component', () => {
  const React = require('react');
  const { View, TextInput, Pressable, Text } = require('react-native');
  
  return {
    MyComponent: ({ onSubmit }) => {
      const { useForm } = require('react-hook-form');
      const { setValue, handleSubmit } = useForm();
      
      return (
        <View>
          <TextInput onChangeText={t => setValue('field', t)} testID="input" />
          <Pressable onPress={handleSubmit(onSubmit)} testID="submit" />
        </View>
      );
    }
  };
});
```
Atau test interaksi langsung dengan `fireEvent.changeText` pada input yang dibungkus `Controller`. Pastikan menggunakan `await waitFor` karena update state RHF bersifat asinkron.

## 5. Keuntungan Migrasi Ini
1. **Performance**: Mengurangi re-render pada parent component saat user mengetik.
2. **Type Safety**: TypeScript otomatis mengetahui tipe data form dari skema Zod.
3. **Maintainability**: Logika validasi terpisah dari UI, mudah diubah tanpa menyentuh render logic.
4. **Testing**: Lebih mudah ditest karena validasi adalah pure function (Zod schema).

---
*Dibuat otomatis oleh AI Assistant - 2026*
