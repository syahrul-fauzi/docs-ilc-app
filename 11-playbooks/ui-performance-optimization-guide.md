# 📱 UI Performance Optimization Guide - ILC-APP

Dokumen ini menjelaskan standar dan best practices untuk optimasi performa UI, animasi, dan rendering pada aplikasi mobile ILC-APP guna mencapai target **60fps** yang konsisten.

---

## 1. Filosofi Performa
Aplikasi hukum memerlukan presisi, namun pengalaman pengguna (UX) yang lambat akan mengurangi tingkat kepercayaan. Kita mengadopsi pendekatan **Adaptive Performance**: memberikan pengalaman visual terbaik pada perangkat high-end, dan pengalaman fungsional yang stabil pada perangkat low-end.

## 2. Low-Performance Mode (Fallback)
Gunakan `performanceService` untuk mendeteksi kemampuan perangkat dan menyesuaikan rendering secara kondisional.

### Implementasi Dasar
```typescript
import { performanceService } from '@/shared/libs/performance';

const MyComponent = () => {
  const isLowPerf = useMemo(() => performanceService.canRenderHeavyGlows() === false, []);
  
  return (
    <View>
      {isLowPerf ? (
        <StaticComponent />
      ) : (
        <Animated.View entering={FadeInDown}>
          <StaticComponent />
        </Animated.View>
      )}
    </View>
  );
};
```

## 3. Best Practices Fase 3 (Advanced)

### 3.1 Pola Utility Rendering
Untuk menjaga keterbacaan kode saat menggunakan banyak fallback, gunakan pola fungsi pembantu:

```typescript
const renderAnimatedContainer = (content: React.ReactNode, delay: number = 0) => {
  if (isLowPerf) return <View className="flex-1">{content}</View>;
  
  return (
    <Animated.View 
      entering={FadeInDown.delay(delay).duration(400)}
      className="flex-1"
    >
      {content}
    </Animated.View>
  );
};
```

### 3.2 Optimasi Modal & Overlay
Modal seringkali menjadi bottleneck karena memuat seluruh subtree saat `visible={true}`.
- **Lazy Content**: Hanya render isi modal jika `visible` true.
- **Simple Animations**: Gunakan `animationType="none"` pada mode low-perf untuk transisi instan.
- **Memoization**: Selalu bungkus modal dengan `React.memo` dan memoize fungsi `onSubmit`/`onClose`.

### 3.3 Haptic Feedback Kondisional
Haptic feedback dapat menyebabkan jitter pada perangkat low-end jika dipicu terlalu sering.
```typescript
const triggerHaptic = () => {
  if (!isLowPerf) {
    Haptics.impactAsync(Haptics.ImpactFeedbackStyle.Light);
  }
};
```

## 4. Optimasi FlatList
`FlatList` adalah komponen paling kritis untuk performa feed dan chat.

### Best Practices:
1.  **Gunakan memo pada renderItem**: Selalu bungkus komponen item dengan `React.memo`.
2.  **getItemLayout**: Implementasikan jika tinggi item bersifat statis atau dapat diprediksi.
3.  **Windowing**: Sesuaikan `windowSize` (3-5) dan `maxToRenderPerBatch` (5-10).
4.  **removeClippedSubviews**: Set ke `true` untuk menghemat memori.

## 5. Checklist Verifikasi Performa
- [ ] **Target 60fps**: FPS stabil di angka 55-60 pada perangkat mid-range.
- [ ] **Memory Leak**: Tidak ada kenaikan memori yang signifikan setelah 10 menit penggunaan chat.
- [ ] **Low-Perf Fallback**: Bayangan kompleks, blur, dan animasi transisi dinonaktifkan pada perangkat < 4GB RAM.
- [ ] **Interaction Latency**: Respon tombol < 100ms.
- [ ] **Accessibility**: Label tetap tersedia meskipun komponen diubah menjadi statis.

---
*Dikelola oleh Tim Lawyers Hub - Terakhir Diperbarui: 2026-01-19*
