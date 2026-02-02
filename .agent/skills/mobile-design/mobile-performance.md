# Mobil Performans Referansı

> React Native ve Flutter performans optimizasyonu, 60fps animasyonlar, bellek yönetimi ve pil değerlendirmeleri üzerine derin dalış.
> **Bu dosya, YZ tarafından üretilen kodların BAŞARISIZ olduğu en önemli konuyu kapsar.**

---

## 1. Mobil Performans Zihniyeti

### Mobil Performansı Neden Farklıdır?

```
MASAÜSTÜ:                          MOBİL:
├── Sınırsız güç                  ├── Pil önemlidir
├── Bol miktarda RAM              ├── RAM paylaşımlıdır, sınırlıdır
├── Kararlı ağ                    ├── Ağ güvenilmezdir
├── CPU her zaman kullanılabilir  ├── CPU ısındığında hızı düşürür (throttle)
└── Kullanıcı zaten hızlı bekler  └── Kullanıcı ANINDA yanıt bekler
```

### Performans Bütçesi Kavramı

```
Her kare (frame) şu sürede tamamlanmalıdır:
├── 60fps → Kare başına 16.67ms
├── 120fps (ProMotion) → Kare başına 8.33ms

Kodunuz daha uzun sürerse:
├── Kare düşmesi → Takılan (janky) kaydırma/animasyon
├── Kullanıcı "yavaş" veya "bozuk" olarak algılar
└── Uygulamanızı SİLECEKLERDİR
```

---

## 2. React Native Performansı

### 🚫 1 Numaralı YZ Hatası: Listeler İçin ScrollView

```javascript
// ❌ ASLA YAPMAYIN - YZ'lerin en sevdiği hata
<ScrollView>
  {items.map(item => (
    <ItemComponent key={item.id} item={item} />
  ))}
</ScrollView>

// Neden felakettir:
// ├── TÜM öğeleri anında render eder (1000 öğe = 1000 render)
// ├── Bellek patlar
// ├── İlk render saniyeler sürer
// └── Kaydırma takılmaya başlar

// ✅ HER ZAMAN FlatList KULLANIN
<FlatList
  data={items}
  renderItem={renderItem}
  keyExtractor={item => item.id}
/>
```

### FlatList Optimizasyon Kontrol Listesi

```javascript
// ✅ DOĞRU: Tüm optimizasyonlar uygulanmış

// 1. Öğe bileşenini memoize edin
const ListItem = React.memo(({ item }: { item: Item }) => {
  return (
    <Pressable style={styles.item}>
      <Text>{item.title}</Text>
    </Pressable>
  );
});

// 2. renderItem'ı useCallback ile memoize edin
const renderItem = useCallback(
  ({ item }: { item: Item }) => <ListItem item={item} />,
  [] // Boş deps = asla yeniden oluşturulmaz
);

// 3. Kararlı keyExtractor (ASLA indis kullanmayın!)
const keyExtractor = useCallback((item: Item) => item.id, []);

// 4. Sabit yükseklikteki öğeler için getItemLayout sağlayın
const getItemLayout = useCallback(
  (data: Item[] | null, index: number) => ({
    length: ITEM_HEIGHT, // Sabit yükseklik
    offset: ITEM_HEIGHT * index,
    index,
  }),
  []
);

// 5. FlatList'e uygulayın
<FlatList
  data={items}
  renderItem={renderItem}
  keyExtractor={keyExtractor}
  getItemLayout={getItemLayout}
  // Performans propları
  removeClippedSubviews={true} // Android: ekran dışını ayır
  maxToRenderPerBatch={10} // Batch başına öğe
  windowSize={5} // Render penceresi (5 = her iki yanda 2 ekran)
  initialNumToRender={10} // Başlangıç öğe sayısı
  updateCellsBatchingPeriod={50} // Batchleme gecikmesi
/>
```

### Her Optimizasyon Neden Önemlidir?

| Optimizasyon | Neyi Önler? | Etki |
|--------------|------------------|--------|
| `React.memo` | Üst bileşen değişiminde re-render | 🔴 Kritik |
| `useCallback renderItem` | Her render'da yeni fonksiyon | 🔴 Kritik |
| Kararlı `keyExtractor` | Yanlış öğe geri dönüşümü (recycling) | 🔴 Kritik |
| `getItemLayout` | Asenkron layout hesaplaması | 🟡 Yüksek |
| `removeClippedSubviews` | Ekran dışı öğelerin bellek yükü | 🟡 Yüksek |
| `maxToRenderPerBatch` | Ana thread'in bloklanması | 🟢 Orta |
| `windowSize` | Bellek kullanımı | 🟢 Orta |

---

### FlashList: Daha İyi Bir Seçenek

```javascript
// Daha iyi performans için FlashList'i değerlendirin
import { FlashList } from "@shopify/flash-list";

<FlashList
  data={items}
  renderItem={renderItem}
  estimatedItemSize={ITEM_HEIGHT}
  keyExtractor={keyExtractor}
/>

// FlatList'e göre avantajları:
// ├── Daha hızlı geri dönüşüm (recycling)
// ├── Daha iyi bellek yönetimi
// ├── Daha basit API
// └── Daha az optimizasyon prop'una ihtiyaç duyması
```

### Animasyon Performansı

```javascript
// ❌ JS tabanlı animasyon (JS thread'ini bloklar)
Animated.timing(value, {
  toValue: 1,
  duration: 300,
  useNativeDriver: false, // KÖTÜ!
}).start();

// ✅ Native-driver animasyon (UI thread'inde çalışır)
Animated.timing(value, {
  toValue: 1,
  duration: 300,
  useNativeDriver: true, // İYİ!
}).start();

// Native driver SADECE şunları destekler:
// ├── transform (translate, scale, rotate)
// └── opacity
// 
// Şunları DESTEKLEMEZ:
// ├── width, height
// ├── backgroundColor
// ├── borderRadius değişiklikleri
// └── margin, padding
```

---

## 3. Flutter Performansı

### 🚫 1 Numaralı YZ Hatası: setState'in Aşırı Kullanımı

```dart
// ❌ YANLIŞ: setState TÜM widget ağacını yeniden oluşturur
class BadCounter extends StatefulWidget {
  @override
  State<BadCounter> createState() => _BadCounterState();
}

class _BadCounterState extends State<BadCounter> {
  int _counter = 0;
  
  void _increment() {
    setState(() {
      _counter++; // Bu, altındaki HER ŞEYİ yeniden oluşturur!
    });
  }
  
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Sayaç: $_counter'),
        ExpensiveWidget(), // Gereksiz yere yeniden oluşur!
        AnotherExpensiveWidget(), // Gereksiz yere yeniden oluşur!
      ],
    );
  }
}
```

### `const` Constructor Devrimi

```dart
// ✅ DOĞRU: const yeniden oluşturmayı (rebuild) engeller

class GoodCounter extends StatefulWidget {
  const GoodCounter({super.key}); // CONST constructor!
  
  @override
  State<GoodCounter> createState() => _GoodCounterState();
}

class _GoodCounterState extends State<GoodCounter> {
  int _counter = 0;
  
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Sayaç: $_counter'),
        const ExpensiveWidget(), // Yeniden oluşmaz!
        const AnotherExpensiveWidget(), // Yeniden oluşmaz!
      ],
    );
  }
}

// KURAL: State'e bağlı olmayan HER widget'a `const` ekleyin
```

### Hedeflenmiş State Yönetimi

```dart
// ❌ setState tüm ağacı yeniden oluşturur
setState(() => _value = newValue);

// ✅ ValueListenableBuilder: cerrahi müdahale ile yeniden oluşturma
class TargetedState extends StatelessWidget {
  final ValueNotifier<int> counter = ValueNotifier(0);
  
  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        // Sayaç değiştiğinde sadece burası yeniden oluşur
        ValueListenableBuilder<int>(
          valueListenable: counter,
          builder: (context, value, child) => Text('$value'),
          child: const Icon(Icons.star), // Yeniden oluşmaz!
        ),
        const ExpensiveWidget(), // Asla yeniden oluşmaz
      ],
    );
  }
}
```

---

## 4. Animasyon Performansı (Her İki Platform)

### 60fps Zorunluluğu

```
İnsan gözü şunu algılar:
├── < 24 fps → "Slayt gösterisi" (bozuk)
├── 24-30 fps → "Takılan" (rahatsız edici)
├── 30-45 fps → "Gözle görülür şekilde akıcı değil"
├── 45-60 fps → "Akıcı" (kabul edilebilir)
├── 60 fps → "Kaymak gibi" (hedef)
└── 120 fps → "Premium" (ProMotion cihazlar)

ASLA 60fps altı animasyon yayınlamayın.
```

### GPU vs CPU Animasyonu

```
GPU HIZLANDIRMALI (HIZLI):        CPU BAĞIMLI (YAVAŞ):
├── transform: translate          ├── width, height
├── transform: scale              ├── top, left, right, bottom
├── transform: rotate             ├── margin, padding
├── opacity                       ├── border-radius (animasyonlu)
└── (Composited, ana thread dışı) └── box-shadow (animasyonlu)

KURAL: Sadece transform ve opacity'yi anime edin.
Diğer her şey düzen (layout) hesaplamasına neden olur.
```

---

## 5. Bellek Yönetimi

### Yaygın Bellek Sızıntıları (Memory Leaks)

| Kaynak | Platform | Çözüm |
|--------|----------|----------|
| Zamanlayıcılar | Her ikisi | cleanup/dispose içinde temizle |
| Event listener'lar | Her ikisi | cleanup/dispose içinde kaldır |
| Abonelikler | Her ikisi | cleanup/dispose içinde iptal et |
| Büyük görseller | Her ikisi | Önbelleği sınırla, yeniden boyutlandır |
| Unmount sonrası asenkron | RN | isMounted kontrolü veya AbortController |
| Animasyon controller | Flutter | Controller'ı dispose et |

---

## 6. Pil Optimizasyonu

### Pil Tüketim Kaynakları

| Kaynak | Etki | İyileştirme |
|--------|--------|------------|
| **Ekran açık** | 🔴 En yüksek | OLED'de karanlık mod |
| **Sürekli GPS** | 🔴 Çok yüksek | "Önemli değişiklik" (significant change) kullan |
| **Ağ istekleri** | 🟡 Yüksek | Gruplandır (batch), agresif önbellekle |
| **Animasyonlar** | 🟡 Orta | Düşük pilde azalt |
| **Arka plan işleri** | 🟡 Orta | Kritik olmayanı ertele |
| **CPU hesaplaması**| 🟢 Düşük | Backend'e devret |

---

## 7. Ağ Performansı

### Önce-Çevrimdışı (Offline-First) Mimarisi

```
                    ┌──────────────┐
                    │      UI      │
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │  Önbellek    │ ← ÖNCE önbellekten oku
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │      Ağ      │ ← Önbelleği ağdan güncelle
                    └──────────────┘

Avantajları:
├── Anında UI (önbellekteki veri için yükleme spinner'ı yok)
├── Çevrimdışı çalışır
├── Veri kullanımını azaltır
├── Yavaş ağlarda daha iyi UX sunar
```

---

## 8. Performans Testi

### Neyi Test Etmeli?

| Metrik | Hedef | Araç |
|--------|--------|------|
| **Kare hızı** | ≥ 60fps | Performance overlay |
| **Bellek** | Kararlı, artış yok | Profiler |
| **Cold start** | < 2s | Manuel zamanlama |
| **TTI (Etkileşim Süresi)** | < 3s | Lighthouse |
| **Liste kaydırma** | Takılma yok | Manuel his |
| **Animasyon akıcılığı** | Kare düşmesi yok | Performance monitor |

### Gerçek Cihazlarda Test Edin

```
⚠️ ASLA sadece şunlara güvenmeyin:
├── Simülatör/emülatör (gerçekten daha hızlıdır)
├── Dev mod (release'den daha yavaştır)
├── Sadece yüksek segment cihazlar

✅ HER ZAMAN şunlarda test edin:
├── Düşük segment Android (< 7000 TL telefon)
├── Eski iOS cihazı (iPhone 8 veya SE)
├── Release/profile build
└── Gerçek verilerle (10 öğeyle değil)
```

---

> **Unutma:** Performans bir optimizasyon değil, temel kalitedir. Yavaş bir uygulama bozuk bir uygulamadır. Elinizdeki en iyi cihazda değil, kullanıcılarınızın elindeki en kötü cihazda test edin.
