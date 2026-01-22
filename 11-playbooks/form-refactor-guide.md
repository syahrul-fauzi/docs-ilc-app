# 📋 Form Refactor Guide: Zod & React Hook Form

Panduan ini menjelaskan standar baru untuk implementasi formulir di **ILC-APP** menggunakan **Zod** untuk validasi dan **React Hook Form** untuk manajemen state.

## 1. Rasionalitas
Sebelumnya, formulir menggunakan `useState` manual dan logika validasi yang tersebar. Standar baru ini memberikan:
- **Type Safety**: Skema Zod meng-infer tipe data TypeScript secara otomatis.
- **Performance**: Mengurangi re-render dengan sistem *uncontrolled components* dari React Hook Form.
- **Consistency**: Pesan error dan aturan validasi didefinisikan secara terpusat.
- **Maintainability**: Memisahkan logika validasi (schema) dari tampilan (UI).

## 2. Struktur File
Setiap fitur yang memiliki formulir wajib mengikuti struktur berikut:
- `model/<feature>.schema.ts`: Definisi skema Zod dan tipe data.
- `ui/<FormName>.tsx`: Komponen UI yang menggunakan skema tersebut.

## 3. Implementasi Skema (Zod)
Buat skema di dalam folder `model/`:

```typescript
import { z } from 'zod';

export const loginSchema = z.object({
  email: z.string().min(1, 'Email wajib diisi').email('Format email tidak valid'),
  password: z.string().min(8, 'Password minimal 8 karakter'),
  rememberMe: z.boolean().default(false),
});

export type LoginFormData = z.infer<typeof loginSchema>;
```

## 4. Implementasi Komponen (React Hook Form)
Gunakan `Controller` untuk mengintegrasikan komponen UI kustom (`Input`, `Checkbox`, dll).

```tsx
import { useForm, Controller } from 'react-hook-form';
import { zodResolver } from '@hookform/resolvers/zod';
import { loginSchema, LoginFormData } from '../model/auth.schema';

export const LoginForm = () => {
  const { control, handleSubmit, formState: { errors, isValid } } = useForm<LoginFormData>({
    resolver: zodResolver(loginSchema),
    defaultValues: { email: '', password: '', rememberMe: false },
    mode: 'onBlur',
  });

  const onSubmit = (data: LoginFormData) => {
    // Logika submit
  };

  return (
    <View>
      <Controller
        control={control}
        name="email"
        render={({ field: { onChange, onBlur, value } }) => (
          <Input
            value={value}
            onChangeText={onChange}
            onBlur={onBlur}
            error={errors.email?.message}
          />
        )}
      />
      {/* ... field lainnya */}
      <Button onPress={handleSubmit(onSubmit)} disabled={!isValid}>
        <Text>Login</Text>
      </Button>
    </View>
  );
};
```

## 5. Standar Validasi Baru
1. **Mode Validasi**: Gunakan `mode: 'onBlur'` untuk formulir panjang dan `mode: 'onChange'` untuk input real-time (seperti post/chat).
2. **Confirm Password**: Gunakan `.refine()` pada Zod untuk validasi kesesuaian password.
3. **Pesan Error**: Gunakan kunci i18n atau pesan yang user-friendly dalam bahasa Indonesia.

## 6. Pengujian (Unit Test)
Setiap formulir baru wajib memiliki test case untuk:
- Validasi input (error muncul saat data tidak valid).
- Kondisi tombol submit (disabled saat tidak valid).
- Pemanggilan API/fungsi submit saat data valid.

## 7. Komponen yang Telah Direfaktorkan
Berikut adalah daftar komponen utama yang telah dimigrasikan ke standar baru:
- **AI Chat**: `AskInputZone.tsx`, `SearchInputCard.tsx`, `EditMessageModal.tsx`, `FeedbackForm.tsx`, `JustificationForm.tsx`, `AnnotationForm.tsx`, `InterventionModal.tsx`, `UatFeedbackModal.tsx`
- **Consultation**: `ConsultationFormDialog.tsx`
- **Personal Chat**: `ChatInput.tsx`
- **Auth**: `LoginForm.tsx`, `RegisterForm.tsx`, `ForgotPasswordForm.tsx`
- **Community**: `PostInputCard.tsx`
- **Legal Search**: `LegalSearchBar.tsx`

## 8. Tips & Troubleshooting Testing
Saat menguji komponen formulir dengan `react-hook-form`, perhatikan hal berikut:

1. **Polyfill setImmediate**: `react-hook-form` bergantung pada `setImmediate`. Tambahkan polyfill di setup file atau di awal test file.
   ```typescript
   if (typeof setImmediate === 'undefined') {
     global.setImmediate = ((fn: any) => setTimeout(fn, 0)) as any;
   }
   ```

2. **Mocking UI Components**: Selalu mock komponen UI kustom jika mereka memiliki logika internal yang kompleks atau animasi.

3. **Mocking Animations (Reanimated)**: Gunakan mock kustom untuk `react-native-reanimated` jika test gagal karena properti seperti `duration` tidak ditemukan.
   ```typescript
   jest.mock('react-native-reanimated', () => {
     const { View } = require('react-native');
     const createMockAnimation = () => ({
       duration: jest.fn().mockReturnThis(),
       delay: jest.fn().mockReturnThis(),
       springify: jest.fn().mockReturnThis(),
       build: jest.fn(() => () => ({ initialValues: {}, animations: {} })),
     });
     return {
       __esModule: true,
       default: { View },
       View,
       FadeIn: createMockAnimation(),
       // ... mock lainnya
     };
   });
   ```

4. **Testing validation errors**: Gunakan `fireEvent.blur` untuk memicu validasi jika menggunakan `mode: 'onBlur'`. Gunakan `waitFor` untuk menunggu pesan error muncul.
   ```typescript
   jest.mock('@/shared/components/ui', () => {
     const React = require('react');
     const { View, TextInput } = require('react-native');
     return {
       Input: React.forwardRef(({ error, ...props }: any, ref: any) => (
         <View>
           <TextInput {...props} ref={ref} />
           {error && <View testID="error-message" />}
         </View>
       )),
       // ... mock lainnya
     };
   });
   ```

2. **Async act & waitFor**: Karena `react-hook-form` memproses validasi secara asinkron, gunakan `act` dan `waitFor` dari `@testing-library/react-native`.
   ```typescript
   await act(async () => {
     fireEvent.press(submitButton);
   });
   await waitFor(() => {
     expect(mockOnSubmit).toHaveBeenCalled();
   });
   ```

3. **Accessibility Labels**: Gunakan `accessibilityLabel` untuk mempermudah pencarian elemen dalam test tanpa bergantung pada struktur UI yang rapuh.

---
*Update Terakhir: 2026-01-21*
