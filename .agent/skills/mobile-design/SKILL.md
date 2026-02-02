---
name: mobile-design
description: iOS ve Android uygulamaları için mobil öncelikli tasarım düşüncesi ve karar verme. Dokunmatik etkileşim, performans desenleri, platform kuralları. Sabit değerler yerine prensipleri öğretir. React Native, Flutter veya yerel (native) mobil uygulamalar oluştururken kullanın.
allowed-tools: Read, Glob, Grep, Bash
---

# Mobil Tasarım Sistemi

> **Felsefe:** Önce dokunmatik. Pil bilincinde. Platforma saygılı. Çevrimdışı çalışabilen.
> **Temel Prensip:** Mobil, küçük bir masaüstü DEĞİLDİR. Mobil kısıtlamaları DÜŞÜNÜN, platform seçimini SORUN.

---

## 🔧 Çalışma Zamanı Scriptleri

**Doğrulama için bunları çalıştırın (okumayın, sadece çalıştırın):**

| Script | Amaç | Kullanım |
|--------|---------|-------|
| `scripts/mobile_audit.py` | Mobil UX ve Dokunmatik Denetimi | `python scripts/mobile_audit.py <proje_yolu>` |

---

## 🔴 ZORUNLU: Çalışmaya Başlamadan Önce Referans Dosyaları Okuyun!

**⛔ İlgili dosyaları okumadan geliştirmeye BAŞLAMAYIN:**

### Evrensel (Her Zaman Okunmalı)

| Dosya | İçerik | Durum |
|------|---------|--------|
| **[mobile-design-thinking.md](mobile-design-thinking.md)** | **⚠️ EZBERLEME KARŞITI: Düşünmeye zorlar, YZ varsayılanlarını engeller** | **⬜ ÖNCELİKLİ KRİTİK** |
| **[touch-psychology.md](touch-psychology.md)** | **Fitts Yasası, jestler, haptik, başparmak bölgesi** | **⬜ KRİTİK** |
| **[mobile-performance.md](mobile-performance.md)** | **RN/Flutter performansı, 60fps, bellek** | **⬜ KRİTİK** |
| **[mobile-backend.md](mobile-backend.md)** | **Push bildirimleri, çevrimdışı senkronizasyon, mobil API** | **⬜ KRİTİK** |
| **[mobile-testing.md](mobile-testing.md)** | **Test piramidi, E2E, platforma özgü** | **⬜ KRİTİK** |
| **[mobile-debugging.md](mobile-debugging.md)** | **Native vs JS hata ayıklama, Flipper, Logcat** | **⬜ KRİTİK** |
| [mobile-navigation.md](mobile-navigation.md) | Tab/Stack/Drawer, derin linkleme (deep linking) | ⬜ Oku |
| [mobile-typography.md](mobile-typography.md) | Sistem fontları, Dinamik Tip, a11y | ⬜ Oku |
| [mobile-color-system.md](mobile-color-system.md) | OLED, karanlık mod, pil duyarlılığı | ⬜ Oku |
| [decision-trees.md](decision-trees.md) | Framework/state/storage seçimi | ⬜ Oku |

> 🧠 **mobile-design-thinking.md EN ÖNCELİKLİDİR!** Bu dosya, YZ'nin ezberlenmiş desenleri kullanmak yerine düşünmesini sağlar.

### Platforma Özgü (Hedefe Göre Okunmalı)

| Platform | Dosya | İçerik | Ne Zaman Okunmalı |
|----------|------|---------|--------------|
| **iOS** | [platform-ios.md](platform-ios.md) | İnsan Arayüzü Yönergeleri (HIG), SF Pro, SwiftUI desenleri | iPhone/iPad için geliştirme yaparken |
| **Android** | [platform-android.md](platform-android.md) | Material Design 3, Roboto, Compose desenleri | Android için geliştirme yaparken |
| **Cross-Platform** | Yukarıdakilerin her ikisi | Platform farklılık noktaları | React Native / Flutter |

> 🔴 **iOS için geliştirme yapıyorsanız → ÖNCE platform-ios.md dosyasını okuyun!**
> 🔴 **Android için geliştirme yapıyorsanız → ÖNCE platform-android.md dosyasını okuyun!**
> 🔴 **Cross-platform ise → HER İKİSİNİ de okuyun ve koşullu platform mantığını uygulayın!**

---

## ⚠️ KRİTİK: VARSAYIMDA BULUNMADAN ÖNCE SORUN (ZORUNLU)

> **DUR! Kullanıcının isteği ucu açıksa, kendi favorilerinize varsayılan olarak dönmeyin.**

### Belirtilmemişse Şunları SORMALSINIZ:

| Konu | Ne Sorulmalı? | Neden? |
|--------|-----|-----|
| **Platform** | "iOS, Android mi yoksa her ikisi mi?" | HER tasarım kararını etkiler |
| **Framework** | "React Native, Flutter mı yoksa native mi?" | Desenleri ve araçları belirler |
| **Navigasyon** | "Tab bar, drawer mı yoksa stack tabanlı mı?" | Temel UX kararıdır |
| **State** | "Hangi state yönetimi? (Zustand/Redux/Riverpod/BLoC?)" | Mimari temelidir |
| **Çevrimdışı** | "Çevrimdışı (offline) çalışma gereksinimi var mı?" | Veri stratejisini etkiler |
| **Hedef Cihazlar** | "Sadece telefon mu, yoksa tablet desteği de var mı?" | Düzen (layout) karmaşıklığı |

### ⛔ YZ MOBİL ANTİ-DESENLERİ (YASAK LİSTESİ)

> 🚫 **Bunlar, YZ'nin kaçınılması gereken varsayılan eğilimleridir!**

#### Performans Günahları

| ❌ ASLA YAPMA | Neden Yanlış? | ✅ HER ZAMAN YAP |
|-------------|----------------|--------------|
| **Uzun listeler için ScrollView** | TÜM öğeleri render eder, bellek patlar | `FlatList` / `FlashList` / `ListView.builder` kullan |
| **Inline renderItem fonksiyonu** | Her render'da yeni fonksiyon, tüm öğeler re-render olur | `useCallback` + `React.memo` |
| **Eksik keyExtractor** | İndis tabanlı keyler sıralamada hatalara neden olur | Veriden gelen benzersiz, kararlı bir ID |
| **getItemLayout'u atlamak** | Asenkron düzen = takılan (janky) kaydırma | Öğeler sabit yükseklikteyse bunu sağlayın |
| **Her yerde setState()** | Gereksiz widget yeniden oluşturma | Hedeflenmiş state, `const` constructor'lar |
| **Native driver: false** | Animasyonlar JS thread tarafından engellenir | Her zaman `useNativeDriver: true` |
| **Prodüksiyonda console.log** | JS thread'ini ciddi şekilde engeller | Release build almadan önce kaldırın |
| **React.memo/const atlamak** | Herhangi bir değişiklikte her öğe re-render olur | Liste öğelerini HER ZAMAN memoize edin |

#### Dokunmatik/UX Günahları

| ❌ ASLA YAPMA | Neden Yanlış? | ✅ HER ZAMAN YAP |
|-------------|----------------|--------------|
| **Dokunmatik hedef < 44px** | İsabetli dokunmak imkansızdır, sinir bozucudur | Minimum 44pt (iOS) / 48dp (Android) |
| **Hedefler arası boşluk < 8px** | Yanındaki öğeye yanlışlıkla dokunma | Minimum 8-12px boşluk |
| **Sadece jestle etkileşim** | Motor becerisi kısıtlı kullanıcılar dışlanır | Her zaman buton alternatifi sunun |
| **Yükleme durumu yok** | Kullanıcı uygulamanın çöktüğünü düşünür | HER ZAMAN yükleme (loading) geri bildirimi gösterin |
| **Hata durumu yok** | Kullanıcı tıkanır, kurtarma yolu yoktur | Yeniden deneme seçeneğiyle hatayı gösterin |
| **Çevrimdışı yönetimi yok** | Ağ kesildiğinde çökme/donma | Kademeli bozulma (graceful degradation), önbelleğe alınmış veri |
| **Platform kurallarını yoksay** | Kullanıcıların kafası karışır, kas hafızası bozulur | iOS, iOS gibi; Android, Android gibi hissettirmeli |

#### Güvenlik Günahları

| ❌ ASLA YAPMA | Neden Yanlış? | ✅ HER ZAMAN YAP |
|-------------|----------------|--------------|
| **AsyncStorage'da Token** | Kolayca erişilebilir, root'lu cihazda çalınabilir | `SecureStore` / `Keychain` / `EncryptedSharedPreferences` |
| **API Anahtarını Hardcode et** | APK/IPA'dan tersine mühendislik yapılabilir | Ortam değişkenleri, güvenli depolama |
| **SSL pinning atlamak** | MITM saldırıları mümkün olabilir | Prodüksiyonda sertifikaları pinleyin |
| **Hassas veri kaydetme (log)** | Loglar dışarı çekilebilir | Tokenları, şifreleri, PII verilerini asla loglamayın |

#### Mimari Günahları

| ❌ ASLA YAPMA | Neden Yanlış? | ✅ HER ZAMAN YAP |
|-------------|----------------|--------------|
| **UI içinde iş mantığı** | Test edilemez, bakımı yapılamaz | Servis katmanı ayrımı |
| **Her şey için global state** | Gereksiz re-render'lar, karmaşıklık | Varsayılan yerel state, gerekirse yukarı taşı |
| **Deep linking'i sona bırak** | Bildirimler, paylaşımlar bozulur | İlk günden deep link'leri planlayın |
| **Dispose/Cleanup atlamak** | Bellek sızıntıları, zombi listener'lar | Abonelikleri, zamanlayıcıları temizleyin |

---

## 📱 Platform Karar Matrisi

### Ne Zaman Birleştirilmeli vs Ne Zaman Ayrılmalı

```
                      BİRLEŞTİR (her ikisinde aynı)  AYIR (platforma özgü)
                      ───────────────────           ──────────────────────────
İş Mantığı            ✅ Her zaman                  -
Veri Katmanı          ✅ Her zaman                  -
Temel Özellikler      ✅ Her zaman                  -
                    
Navigasyon            -                             ✅ iOS: kenar kaydırma, Android: geri butonu
Jestler                -                             ✅ Platform-native hissi
İkonlar               -                             ✅ SF Symbols vs Material Icons
Tarih Seçiciler       -                             ✅ Yerel seçiciler (picker) daha iyi hissettirir
Modallar/Sayfalar     -                             ✅ iOS: bottom sheet vs Android: dialog
Tipografi             -                             ✅ SF Pro vs Roboto (veya özel)
Hata Diyalogları      -                             ✅ Alertler için platform kuralları
```

### Hızlı Referans: Platform Varsayılanları

| Öğe | iOS | Android |
|---------|-----|---------|
| **Birincil Yazı Tipi** | SF Pro / SF Compact | Roboto |
| **Min. Dokunmatik Hedef** | 44pt × 44pt | 48dp × 48dp |
| **Geri Navigasyon** | Sol kenardan kaydırma | Sistem geri butonu/jest |
| **Tab Bar İkonları** | SF Symbols | Material Symbols |
| **Aksiyon Sayfası** | Alttan UIActionSheet | Bottom Sheet / Dialog |
| **İlerleme (Progress)** | Spinner (Dönerge) | Çizgisel ilerleme (Material) |
| **Çek-Yenile** | Native UIRefreshControl | SwipeRefreshLayout |

---

## 🧠 Mobil UX Psikolojisi (Hızlı Referans)

### Dokunmatik İçin Fitts Yasası

```
Masaüstü: İmleç hassastır (1px)
Mobil:    Parmak hassas değildir (~7mm temas alanı)

→ Dokunmatik hedefler minimum 44-48px OLMALI
→ Önemli eylemler BAŞPARMAK BÖLGESİNDE (ekranın altı) olmalı
→ Yıkıcı eylemler kolay erişimden UZAKTA olmalı
```

### Başparmak Bölgesi (Tek El Kullanımı)

```
┌─────────────────────────────┐
│      ERİŞİMİ ZOR            │ ← Navigasyon, menü, geri
│        (uzanma)             │
├─────────────────────────────┤
│      ERİŞİMİ NORMAL         │ ← İkincil eylemler
│        (doğal)              │
├─────────────────────────────┤
│      ERİŞİMİ KOLAY          │ ← BİRİNCİL CTA'lar, tab bar
│  (başparmağın doğal yayı)    │ ← Ana içerik etkileşimi
└─────────────────────────────┘
         [  ANA EKRAN  ]
```

### Mobil-Özel Bilişsel Yük

| Masaüstü | Mobil Farkı |
|---------|-------------------|
| Çoklu pencere | Bir seferde TEK görev |
| Klavye kısayolları | Dokunma jestleri |
| Hover durumları | Hover YOK (dokun ya da dokunma) |
| Geniş ekran | Sınırlı alan, dikey kaydırma |
| Kararlı dikkat | Sürekli kesintiye uğrar |

Detaylı inceleme için: [touch-psychology.md](touch-psychology.md)

---

## ⚡ Performans Prensipleri (Hızlı Referans)

### React Native Kritik Kuralları

```typescript
// ✅ DOĞRU: Memoize edilmiş renderItem + React.memo sarmalayıcısı
const ListItem = React.memo(({ item }: { item: Item }) => (
  <View style={styles.item}>
    <Text>{item.title}</Text>
  </View>
));

const renderItem = useCallback(
  ({ item }: { item: Item }) => <ListItem item={item} />,
  []
);

// ✅ DOĞRU: Tüm optimizasyonlarla birlikte FlatList
<FlatList
  data={items}
  renderItem={renderItem}
  keyExtractor={(item) => item.id}  // Kararlı ID, indis DEĞİL
  getItemLayout={(data, index) => ({
    length: ITEM_HEIGHT,
    offset: ITEM_HEIGHT * index,
    index,
  })}
  removeClippedSubviews={true}
  maxToRenderPerBatch={10}
  windowSize={5}
/>
```

### Flutter Kritik Kuralları

```dart
// ✅ DOĞRU: const constructor'lar yeniden oluşturmayı engeller
class MyWidget extends StatelessWidget {
  const MyWidget({super.key}); // CONST!

  @override
  Widget build(BuildContext context) {
    return const Column( // CONST!
      children: [
        Text('Statik içerik'),
        MyConstantWidget(),
      ],
    );
  }
}

// ✅ DOĞRU: ValueListenableBuilder ile hedeflenmiş state
ValueListenableBuilder<int>(
  valueListenable: counter,
  builder: (context, value, child) => Text('$value'),
  child: const ExpensiveWidget(), // Yeniden oluşmaz!
)
```

### Animasyon Performansı

```
GPU hızlandırmalı (HIZLI):   CPU bağımlı (YAVAŞ):
├── transform                ├── width, height
├── opacity                  ├── top, left, right, bottom
└── (SADECE bunları kullan)  ├── margin, padding
                             └── (Bunları anime etmekten KAÇIN)
```

Tam kılavuz için: [mobile-performance.md](mobile-performance.md)

---

## 📝 KONTROL NOKTASI (Herhangi Bir Mobil İşten Önce ZORUNLU)

> **HERHANGİ bir mobil kod yazmadan önce, bu kontrol noktasını tamamlamalısınız:**

```
🧠 KONTROL NOKTASI:

Platform:    [ iOS / Android / Her İkisi ]
Framework:   [ React Native / Flutter / SwiftUI / Kotlin ]
Okunan Dosyalar: [ Okuduğunuz yetenek dosyalarını listeleyin ]

Uygulayacağım 3 Prensip:
1. _______________
2. _______________
3. _______________

Kaçınacağım 3 Anti-Desen:
1. _______________
2. _______________
```

**Örnek:**
```
🧠 KONTROL NOKTASI:

Platform:    iOS + Android (Cross-platform)
Framework:   React Native + Expo
Okunan Dosyalar: touch-psychology.md, mobile-performance.md, platform-ios.md, platform-android.md

Uygulayacağım 3 Prensip:
1. Tüm listeler için React.memo + useCallback ile FlatList
2. 48px dokunmatik hedefler, birincil CTA'lar için başparmak bölgesi
3. Platforma özgü navigasyon (iOS kenar kaydırma, Android geri butonu)

Kaçınacağım Anti-Desenler:
1. Listeler için ScrollView → FlatList
2. Inline renderItem → Memoized
3. Tokenlar için AsyncStorage → SecureStore
```

> 🔴 **Kontrol noktasını dolduramıyor musunuz? → GERİ DÖNÜN VE YETENEK DOSYALARINI OKUYUN.**

---

## 🔧 Framework Karar Ağacı

```
NE İNŞA EDİYORSUNUZ?
        │
        ├── OTA güncellemeleri + hızlı yineleme + web ekibi ihtiyacı
        │   └── ✅ React Native + Expo
        │
        ├── Pixel-perfect özel UI + kritik performans ihtiyacı
        │   └── ✅ Flutter
        │
        ├── Derin native özellikler + tek platform odaklı
        │   ├── Sadece iOS → SwiftUI
        │   └── Sadece Android → Kotlin + Jetpack Compose
        │
        ├── Mevcut RN kod tabanı + yeni özellikler
        │   └── ✅ React Native (bare workflow)
        │
        └── Kurumsal + mevcut Flutter kod tabanı
            └── ✅ Flutter
```

Tam karar ağaçları için: [decision-trees.md](decision-trees.md)

---

## 📋 Geliştirme Öncesi Kontrol Listesi

### HERHANGİ Bir Mobil Projeye Başlamadan Önce

- [ ] **Platform doğrulandı mı?** (iOS / Android / Her İkisi)
- [ ] **Framework seçildi mi?** (RN / Flutter / Native)
- [ ] **Navigasyon deseni kararlaştırıldı mı?** (Tabs / Stack / Drawer)
- [ ] **State yönetimi seçildi mi?** (Zustand / Redux / Riverpod / BLoC)
- [ ] **Çevrimdışı gereksinimler biliniyor mu?**
- [ ] **Deep linking ilk günden planlandı mı?**
- [ ] **Hedef cihazlar tanımlandı mı?** (Telefon / Tablet / Her İkisi)

### Her Ekrandan Önce

- [ ] **Dokunmatik hedefler ≥ 44-48px mi?**
- [ ] **Birincil CTA başparmak bölgesinde mi?**
- [ ] **Yükleme (loading) durumu mevcut mu?**
- [ ] **Yeniden deneme içeren hata durumu mevcut mu?**
- [ ] **Çevrimdışı yönetimi düşünüldü mü?**
- [ ] **Platform kurallarına uyuldu mu?**

### Yayından (Release) Önce

- [ ] **console.log'lar kaldırıldı mı?**
- [ ] **Hassas veriler için SecureStore kullanıldı mı?**
- [ ] **SSL pinning etkinleştirildi mi?**
- [ ] **Listeler optimize edildi mi (memo, keyExtractor)?**
- [ ] **Unmount anında bellek temizliği yapılıyor mu?**
- [ ] **Düşük donanımlı cihazlarda test edildi mi?**
- [ ] **Tüm etkileşimli öğelerde erişilebilirlik etiketleri (labels) var mı?**

---

## 📚 Referans Dosyaları

Belirli alanlarda daha derin rehberlik için:

| Dosya | Ne Zaman Kullanılır |
|------|-------------|
| [mobile-design-thinking.md](mobile-design-thinking.md) | **ÖNCE! Ezberleme karşıtı, bağlam tabanlı düşünmeye zorlar** |
| [touch-psychology.md](touch-psychology.md) | Dokunmatik etkileşimi, Fitts Yasasını, jest tasarımını anlama |
| [mobile-performance.md](mobile-performance.md) | RN/Flutter optimizasyonu, 60fps, bellek/pil |
| [platform-ios.md](platform-ios.md) | iOS'e özgü tasarım, HIG uyumluluğu |
| [platform-android.md](platform-android.md) | Android'e özgü tasarım, Material Design 3 |
| [mobile-navigation.md](mobile-navigation.md) | Navigasyon desenleri, deep linking |
| [mobile-typography.md](mobile-typography.md) | Yazı tipi ölçeği, sistem fontları, erişilebilirlik |
| [mobile-color-system.md](mobile-color-system.md) | OLED optimizasyonu, karanlık mod, pil |
| [decision-trees.md](decision-trees.md) | Framework, state, depolama kararları |

---

> **Unutma:** Mobil kullanıcılar sabırsızdır, sürekli kesintiye uğrarlar ve küçük ekranlarda hassas olmayan parmaklar kullanırlar. EN KÖTÜ koşullar için tasarım yapın: kötü ağ, tek el, parlak güneş, düşük pil. Orada çalışıyorsa, her yerde çalışır.
