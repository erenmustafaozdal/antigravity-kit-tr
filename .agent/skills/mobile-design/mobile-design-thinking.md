# Mobil Tasarım Düşüncesi (Thinking)

> **Bu dosya, YZ'nin ezberlenmiş desenleri kullanmasını engeller ve gerçek düşünmeye zorlar.**
> Mobil geliştirmede standart YZ eğitim varsayılanlarını engelleme mekanizmalarıdır.
> **Frontend'deki düzen ayrıştırma (layout decomposition) yaklaşımının mobil karşılığıdır.**

---

## 🧠 DERİN MOBİL DÜŞÜNCE PROTOKOLÜ

### Her Mobil Projeden Önce Bu Süreç Zorunludur

```
┌─────────────────────────────────────────────────────────────────┐
│                    DERİN MOBİL DÜŞÜNCE                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1️⃣ BAĞLAM TARAMASI                                             │
│     └── Bu proje için varsayımlarım neler?                      │
│         └── Bu varsayımları SORGULAYIN                          │
│                                                                 │
│  2️⃣ VARSAYILAN KARŞITI ANALİZ                                    │
│     └── Ezberlenmiş bir desen mi uyguluyorum?                   │
│         └── Bu desen GERÇEKTEN BU proje için en iyisi mi?       │
│                                                                 │
│  3️⃣ PLATFORM AYRIŞTIRMA                                          │
│     └── iOS ve Android'i ayrı ayrı düşündüm mü?                 │
│         └── Platforma özgü desenler nelerdir?                   │
│                                                                 │
│  4️⃣ DOKUNMATİK ETKİLEŞİM KIRILIMI                                │
│     └── Her etkileşimi ayrı ayrı analiz ettim mi?               │
│         └── Fitts Yasasını ve Başparmak Bölgesini uyguladım mı?  │
│                                                                 │
│  5️⃣ PERFORMANS ETKİ ANALİZİ                                      │
│     └── Her bileşenin performans etkisini düşündüm mü?          │
│         └── Varsayılan çözüm performanslı mı?                   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🚫 YZ MOBİL VARSAYILANLARI (YASAK LİSTESİ)

### Bu Desenleri Otomatik Olarak Kullanmak YASAKTIR!

Aşağıdaki desenler, YZ'lerin eğitim verilerinden öğrendiği "varsayılanlardır".
Bunlardan herhangi birini kullanmadan önce **onları SORGULAYIN ve ALTERNATİFLERİ DÜŞÜNÜN!**

```
┌─────────────────────────────────────────────────────────────────┐
│                 🚫 YZ MOBİL GÜVENLİ LİMAN                        │
│         (Varsayılan Desenler - Sorgulamadan Asla Kullanma)      │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  NAVİGASYON VARSAYILANLARI:                                     │
│  ├── Her proje için Tab Bar (Drawer daha mı iyi olurdu?)        │
│  ├── Sabit 5 sekme (3 tane yeterli mi? 6+ için Drawer mı?)      │
│  ├── Solda "Ana Sayfa" sekmesi (Kullanıcı davranışı ne diyor?)  │
│  └── Hamburger menü (Artık modası geçti mi?)                     │
│                                                                 │
│  STATE YÖNETİMİ VARSAYILANLARI:                                 │
│  ├── Her yerde Redux (Zustand/Jotai yeterli mi?)                │
│  ├── Her şey için global state (Yerel state yeterli değil mi?)  │
│  ├── Context Provider cehennemi (Atom tabanlı mı daha iyi?)     │
│  └── Her Flutter projesi için BLoC (Riverpod daha mı modern?)   │
│                                                                 │
│  LİSTE UYGULAMA VARSAYILANLARI:                                 │
│  ├── Varsayılan olarak FlatList (FlashList daha mı hızlı?)      │
│  ├── windowSize=21 (Gerçekten gerekli mi?)                      │
│  ├── removeClippedSubviews (Her zaman mı?)                      │
│  └── ListView.builder (ListView.separated daha mı iyi?)         │
│                                                                 │
│  UI DESEN VARSAYILANLARI:                                       │
│  ├── Sağ altta FAB (Sol alt daha mı erişilebilir?)              │
│  ├── Her listede çek-yenile (Her yerde gerekli mi?)              │
│  ├── Soldan kaydır-sil (Sağ taraf daha mı iyi?)                 │
│  └── Her modal için Bottom Sheet (Tam ekran daha mı iyi?)       │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔍 BİLEŞEN AYRIŞTIRMA (ZORUNLU)

### Her Ekran İçin Ayrıştırma Analizi

Herhangi bir ekranı tasarlamadan önce bu analizi gerçekleştirin:

```
EKRAN: [Ekran Adı]
├── BİRİNCİL EYLEM: [Ana eylem nedir?]
│   └── Başparmak bölgesinde mi? [Evet/Hayır → Neden?]
│
├── DOKUNMATİK HEDEFLER: [Tüm tıklanabilir öğeler]
│   ├── [Öğe 1]: [Boyut]pt → Yeterli mi?
│   ├── [Öğe 2]: [Boyut]pt → Yeterli mi?
│   └── Boşluklandırma: [Aralık]pt → Yanlışlıkla dokunma riski?
│
├── KAYDIRILABİLİR İÇERİK:
│   ├── Bu bir liste mi? → FlatList/FlashList [Neden bu seçim?]
│   ├── Öğe sayısı: ~[N] → Performans değerlendirmesi?
│   └── Sabit yükseklik? → getItemLayout gerekli mi?
│
├── STATE GEREKSİNİMLERİ:
│   ├── Yerel state yeterli mi?
│   ├── State'i yukarı taşıyacak mıyım?
│   └── Global state zorunlu mu? [Neden?]
│
├── PLATFORM FARKLILIKLARI:
│   ├── iOS: [Farklı bir şey gerekiyor mu?]
│   └── Android: [Farklı bir şey gerekiyor mu?]
│
├── ÇEVRİMDIŞI DEĞERLENDİRMESİ:
│   ├── Bu ekran çevrimdışı çalışmalı mı?
│   └── Önbellek stratejisi: [Evet/Hayır/Hangisi?]
│
└── PERFORMANS ETKİSİ:
    ├── Ağır bileşenler var mı?
    ├── Memoizasyon gerekli mi?
    └── Animasyon performansı?
```

---

## 🎯 DESEN SORGULAMA MATRİSİ

Her varsayılan desen için bu soruları sorun:

### Navigasyon Deseni Sorgulama

| Varsayım | Soru | Alternatif |
|------------|----------|-------------|
| "Tab bar kullanacağım" | Kaç hedef var? | 3 → minimal sekme, 6+ → drawer |
| "5 sekme" | Hepsi eşit derecede önemli mi? | "Daha Fazla" sekmesi? Drawer hibrit? |
| "Alt navigasyon" | iPad/tablet desteği? | Yan navigasyon (Navigation rail) alternatifi |
| "Stack navigasyon" | Derin linkleri (deep links) düşündüm mü? | URL yapısı = navigasyon yapısı |

### State Deseni Sorgulama

| Varsayım | Soru | Alternatif |
|------------|----------|-------------|
| "Redux kullanacağım" | Uygulama ne kadar karmaşık? | Basitse: Zustand, Sunucu: TanStack |
| "Global state" | Bu state gerçekten global mi? | Yerel taşıma, Context selector |
| "Context Provider" | Re-render sorunu olur mu? | Zustand, Jotai (atom tabanlı) |
| "BLoC deseni" | Boilerplate koduna değer mi? | Riverpod (daha az kod) |

### Liste Deseni Sorgulama

| Varsayım | Soru | Alternatif |
|------------|----------|-------------|
| "FlatList" | Performans kritik mi? | FlashList (daha hızlı) |
| "Standart renderItem" | Memoize edildi mi? | useCallback + React.memo |
| "İndis key" | Veri sırası değişiyor mu? | item.id kullan |
| "ListView" | Ayırıcılar (separators) var mı? | ListView.separated |

### UI Deseni Sorgulama

| Varsayım | Soru | Alternatif |
|------------|----------|-------------|
| "Sağ altta FAB" | Kullanıcının el alışkanlığı? | Erişilebilirlik ayarları |
| "Çek-Yenile" | Bu listenin yenilenmeye ihtiyacı var mı? | Sadece gerekli olduğunda |
| "Modal bottom sheet" | Ne kadar içerik var? | Tam ekran modal daha iyi olabilir |
| "Kaydırma eylemleri" | Keşfedilebilirlik? | Görünür buton alternatifi |

---

## 🧪 EZBERLEME KARŞITI TEST

### Her Çözümden Önce Kendinize Sorun

```
┌─────────────────────────────────────────────────────────────────┐
│                    EZBERLEME KARŞITI KONTROL LİSTESİ            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  □ Bu çözümü "her zaman böyle yaptığım için" mi seçtim?         │
│    → Yanıt EVET ise: DURUN. Alternatifleri değerlendirin.       │
│                                                                 │
│  □ Bu, eğitim verilerinde sıkça gördüğüm bir desen mi?          │
│    → Yanıt EVET ise: BU proje için GERÇEKTEN uygun mu?         │
│                                                                 │
│  □ Bu çözümü düşünmeden, otomatik olarak mı yazdım?             │
│    → Yanıt EVET ise: Geri çekilin, ayrıştırma analizi yapın.    │
│                                                                 │
│  □ Alternatif bir yaklaşım düşündüm mü?                         │
│    → Yanıt HAYIR ise: En az 2 alternatif düşünün, sonra karar verin. │
│                                                                 │
│  □ Platforma özgü düşündüm mü?                                  │
│    → Yanıt HAYIR ise: iOS ve Android'i ayrı ayrı analiz edin.   │
│                                                                 │
│  □ Bu çözümün performans etkisini düşündüm mü?                  │
│    → Yanıt HAYIR ise: Bellek, CPU, pil etkisi nedir?             │
│                                                                 │
│  □ Bu çözüm BU projenin BAĞLAMI için uygun mu?                  │
│    → Yanıt HAYIR ise: Bağlama göre özelleştirin.                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📊 BAĞLAM TABANLI KARAR PROTOKOLÜ

### Proje Türüne Göre Farklı Düşünün

```
PROJE TÜRÜNÜ BELİRLEYİN:
        │
        ├── E-Ticaret Uygulaması
        │   ├── Navigasyon: Tab (Ana Sayfa, Arama, Sepet, Hesap)
        │   ├── Listeler: Ürün ızgaraları (memoize, görsel odaklı)
        │   ├── Performans: Görsel önbellekleme KRİTİK
        │   ├── Çevrimdışı: Sepet kalıcılığı, ürün önbelleği
        │   └── Özel: Ödeme akışı, ödeme güvenliği
        │
        ├── Sosyal/İçerik Uygulaması
        │   ├── Navigasyon: Tab (Akış, Arama, Oluştur, Bildirim, Profil)
        │   ├── Listeler: Sonsuz kaydırma, karmaşık öğeler
        │   ├── Performans: Akış render hızı KRİTİK
        │   ├── Çevrimdışı: Akış önbelleği, taslak gönderiler
        │   └── Özel: Gerçek zamanlı güncellemeler, medya yönetimi
        │
        ├── Verimlilik/SaaS Uygulaması
        │   ├── Navigasyon: Drawer veya adaptif (mobil sekme, tablet ray)
        │   ├── Listeler: Veri tabloları, formlar
        │   ├── Performans: Veri senkronizasyonu
        │   ├── Çevrimdışı: Tam çevrimdışı düzenleme
        │   └── Özel: Çakışma giderme, arka plan senkronizasyonu
        │
        ├── Araç/Utility Uygulaması
        │   ├── Navigasyon: Minimal (sadece stack olabilir)
        │   ├── Listeler: Muhtemelen minimal
        │   ├── Performans: Hızlı açılış
        │   ├── Çevrimdışı: Temel özellik çevrimdışı
        │   └── Özel: Widget, kısayollar
        │
        └── Medya/Streaming Uygulaması
            ├── Navigasyon: Tab (Ana Sayfa, Arama, Kitaplık, Profil)
            ├── Listeler: Yatay karuseller, dikey akışlar
            ├── Performans: Ön yükleme, ara belleğe alma (buffering)
            ├── Çevrimdışı: İndirme yönetimi
            └── Özel: Arka planda oynatma, yansıtma (casting)
```

---

## 🔄 ETKİLEŞİM KIRILIMI

### Her Jest (Gesture) İçin Analiz

Herhangi bir jest eklemeden önce:

```
JEST: [Jest Türü]
├── KEŞFEDİLEBİLİRLİK:
│   └── Kullanıcılar bu jesti nasıl keşfedecek?
│       ├── Görsel bir ipucu var mı?
│       ├── Tanıtım (onboarding) sırasında gösterilecek mi?
│       └── Buton alternatifi var mı? (ZORUNLU)
│
├── PLATFORM KURALLARI:
│   ├── Bu jest iOS'ta ne anlama geliyor?
│   ├── Bu jest Android'de ne anlama geliyor?
│   └── Platform kurallarından sapıyor muyum?
│
├── ERİŞİLEBİLİRLİK:
│   ├── Motor becerisi kısıtlı kullanıcılar bu jesti yapabilir mi?
│   ├── VoiceOver/TalkBack alternatifi var mı?
│   └── Anahtar kontrolü (switch control) ile çalışıyor mu?
│
├── ÇAKIŞMA KONTROLÜ:
│   ├── Sistem jestleriyle çakışıyor mu?
│   │   ├── iOS: Kenar kaydırıp geri gitme
│   │   ├── Android: Geri jesti
│   │   └── Ana ekran çubuğu kaydırması
│   └── Uyguladaki diğer jestlerle uyumlu mu?
│
└── GERİ BİLDİRİM:
    ├── Haptik (titreşim) geri bildirim tanımlandı mı?
    ├── Görsel geri bildirim yeterli mi?
    └── Sesli geri bildirim gerekli mi?
```

---

## 🎭 KONTROL LİSTESİNDEN ÖTE BİR RUH (Mobil Versiyon)

### Kontrol Listesini Geçmek Yeterli Değildir!

| ❌ Öz-Aldatma | ✅ Dürüst Değerlendirme |
|-------------------|----------------------|
| "Dokunmatik hedef 44px" (ama kenarda, ulaşılamaz) | "Kullanıcı buna tek elle ulaşabilir mi?" |
| "FlatList kullandım" (ama memoize etmedim) | "Kaydırma pürüzsüz mü?" |
| "Platforma özgü navigasyon" (ama sadece ikonlar farklı) | "iOS, iOS gibi; Android, Android gibi hissettiriyor mu?" |
| "Çevrimdışı destek var" (ama hata mesajı genel) | "Kullanıcı çevrimdışıyken aslında ne yapabilir?" |
| "Yükleme durumu var" (ama sadece bir spinner) | "Kullanıcı ne kadar bekleyeceğini biliyor mu?" |

> 🔴 **Kontrol listesini geçmek hedef DEĞİLDİR. Harika bir mobil UX oluşturmak HEDEFTİR.**

---

## 📝 MOBİL TASARIM TAAHHÜTNAMESİ

### Her Mobil Projenin Başında Bunu Doldurun

```
📱 MOBİL TASARIM TAAHHÜTNAMESİ

Proje: _______________
Platform: iOS / Android / Her İkisi

1. Bu projede KULLANMAYACAĞIM varsayılan desen:
   └── _______________
   
2. Bu proje için bağlama özel odak noktam:
   └── _______________

3. Uygulayacağım platforma özgü farklılıklar:
   └── iOS: _______________
   └── Android: _______________

4. Performans için özellikle optimize edeceğim alan:
   └── _______________

5. Bu projenin benzersiz zorluğu:
   └── _______________

🧠 Eğer bu taahhütnameyi dolduramıyorsam → Projeyi yeterince iyi anlamamışım demektir.
   → Geri dönün, bağlamı daha iyi anlayın, kullanıcıya sorun.
```

---

## 🚨 ZORUNLU: Her Mobil İşten Önce

```
┌─────────────────────────────────────────────────────────────────┐
│                    İŞ ÖNCESİ DOĞRULAMA                          │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  □ Bileşen Ayrıştırmasını tamamladım mı?                        │
│  □ Desen Sorgulama Matrisini doldurdum mı?                      │
│  □ Ezberleme Karşıtı Testi geçtim mi?                           │
│  □ Bağlam tabanlı kararlar verdim mi?                           │
│  □ Etkileşim Kırılımını analiz ettim mi?                        │
│  □ Mobil Tasarım Taahhütnamesini doldurdum mu?                  │
│                                                                 │
│  ⚠️ Bunları tamamlamadan kod yazmaya başlamayın!                │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

> **Unutma:** Bir çözümü "her zaman böyle yapıldığı için" seçtiyseniz, DÜŞÜNMEDEN seçmişsinizdir. Her proje benzersizdir. Her bağlam farklıdır. Her kullanıcı davranışı spesifiktir. **DÜŞÜNÜN, sonra kodlayın.**
