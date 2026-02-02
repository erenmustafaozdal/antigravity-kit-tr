# Dokunmatik Psikolojisi Referansı

> Mobil dokunmatik etkileşim, dokunma için Fitts Yasası, başparmak bölgesi anatomisi, jest psikolojisi ve haptik (titreşim) geri bildirim konularına derin dalış.
> **Bu, ux-psychology.md dosyasının mobil karşılığıdır - tüm mobil işler için KRİTİKTİR.**

---

## 1. Dokunma İçin Fitts Yasası

### Temel Fark

```
MASAÜSTÜ (Fare/Trackpad):
├── İmleç boyutu: 1 piksel (hassas)
├── Görsel geri bildirim: Hover (üzerine gelme) durumları
├── Hata maliyeti: Düşük (yeniden denemek kolay)
└── Hedefe ulaşım: Hızlı, hassas

MOBİL (Parmak):
├── Temas alanı: ~7mm çap (hassas değil)
├── Görsel geri bildirim: Hover yok, sadece dokunma
├── Hata maliyeti: Yüksek (sinir bozucu tekrarlar)
├── Oklüzyon: Parmak hedefi kapatır
└── Hedefe ulaşım: Daha yavaş, daha büyük hedefler gerektirir
```

### Uyarlanmış Fitts Yasası Formülü

```
Dokunmatik erişim süresi = a + b × log₂(1 + D/W)

Burada:
├── D = Hedefe olan uzaklık
├── W = Hedefin genişliği
└── Dokunma için: W, masaüstüne göre ÇOK daha büyük olmalıdır
```

### Minimum Dokunmatik Hedef Boyutları

| Platform | Minimum | Önerilen | Kullanım Amacı |
|----------|---------|-------------|---------|
| **iOS (HIG)** | 44pt × 44pt | 48pt+ | Tüm tıklanabilir öğeler |
| **Android (Material)** | 48dp × 48dp | 56dp+ | Tüm tıklanabilir öğeler |
| **WCAG 2.2** | 44px × 44px | - | Erişilebilirlik uyumluluğu |
| **Kritik Eylemler** | - | 56-64px | Birincil CTA'lar, yıkıcı eylemler |

### Görsel Boyut vs Tıklama Alanı

```
┌─────────────────────────────────────┐
│                                     │
│    ┌─────────────────────────┐      │
│    │                         │      │
│    │    [  BUTON   ]         │ ← Görsel: 36px
│    │                         │      │
│    └─────────────────────────┘      │
│                                     │ ← Tıklama alanı: 48px (padding ile genişletilmiş)
└─────────────────────────────────────┘

✅ DOĞRU: Tıklama alanı minimum 44-48px ise görsel daha küçük olabilir
❌ YANLIŞ: Tıklama alanını küçük görsel öğeyle aynı boyutta yapmak
```

### Uygulama Kuralları

| Öğe | Görsel Boyut | Tıklama Alanı |
|---------|-------------|----------|
| İkon butonları | 24-32px | 44-48px (dolgu/padding ile) |
| Metin linkleri | Herhangi biri | Minimum 44px yükseklik |
| Liste öğeleri | Tam genişlik | 48-56px yükseklik |
| Checkbox/Radio | 20-24px | 44-48px dokunma alanı |
| Kapat/X butonları | 24px | Minimum 44px |
| Tab bar öğeleri | İkon 24-28px | Tam sekme genişliği, 49px yükseklik (iOS) |

---

## 2. Başparmak Bölgesi Anatomisi

### Tek Elle Telefon Kullanımı

```
Araştırmalar gösteriyor ki: Kullanıcıların %49'u telefonu tek elle tutuyor.

┌─────────────────────────────────────┐
│                                     │
│  ┌─────────────────────────────┐    │
│  │       ERİŞİMİ ZOR           │    │ ← Durum çubuğu, üst navigasyon
│  │      (uzanma gerektirir)    │    │    Şunları koyun: Geri, menü, ayarlar
│  │                             │    │
│  ├─────────────────────────────┤    │
│  │                             │    │
│  │       ERİŞİMİ NORMAL        │    │ ← İçerik alanı
│  │        (konforlu)           │    │    Şunları koyun: İkincil eylemler, içerik
│  │                             │    │
│  ├─────────────────────────────┤    │
│  │                             │    │
│  │       ERİŞİMİ KOLAY         │    │ ← Tab bar, FAB bölgesi
│  │      (başparmak yayı)       │    │    Şunları koyun: BİRİNCİL CTA'lar!
│  │                             │    │
│  └─────────────────────────────┘    │
│                                     │
│          [   ANA EKRAN  ]           │
└─────────────────────────────────────┘
```

### Başparmak Yayı (Sağ Elini Kullanan Kullanıcı)

```
Telefonu sağ elle tutarken:

┌───────────────────────────────┐
│  ZORLANMA     ZORLANMA   OK   │
│                               │
│  ZORLANMA       OK      KOLAY │
│                               │
│    OK          KOLAY    KOLAY │
│                               │
│   KOLAY        KOLAY    KOLAY │
└───────────────────────────────┘

Sol el bunun tam tersidir.
→ HER İKİ el için de tasarlayın veya sağ elin baskın olduğunu varsayın.
```

### Yerleşim Yönergeleri

| Öğe Türü | İdeal Konum | Neden? |
|--------------|----------------|--------|
| **Birincil CTA** | Alt orta/sağ | Kolay başparmak erişimi |
| **Tab bar** | Alt | Doğal başparmak pozisyonu |
| **FAB** | Sağ alt | Sağ el için kolay erişim |
| **Navigasyon** | Üst (uzanma) | Daha az sıklıkta kullanım |
| **Yıkıcı eylemler** | Sol üst | Erişimi zor = yanlışlıkla dokunması zor |
| **Kapat/İptal** | Sol üst | Genel kabul görmüş kural + güvenlik |
| **Onayla/Tamam** | Sağ üst veya alt | Genel kabul görmüş kural |

### Büyük Telefon Değerlendirmeleri (>6")

```
Büyük telefonlarda üst %40'lık alan tek elle kullanım için "ölü bölge" haline gelir.

Çözümler:
├── Erişilebilirlik özellikleri (iOS Reachability)
├── Aşağı çekilebilir arayüzler (içeriği aşağıya çeken yapılar)
├── Alt sayfa (bottom sheet) navigasyonu
├── Yüzen aksiyon butonları (FAB)
├── Üst eylemler için jest tabanlı alternatifler
```

---

## 3. Dokunma vs Tıklama Psikolojisi

### Beklenti Farklılıkları

| Konu | Tıklama (Masaüstü) | Dokunma (Mobil) |
|--------|-----------------|----------------|
| **Geri bildirim süresi**| 100ms bekleyebilir | Anında beklenti (<50ms) |
| **Görsel geri bildirim**| Hover → Tıklama | Anında dokunma yanıtı |
| **Hata toleransı** | Kolay yeniden deneme | Sinir bozucu, bozuk hissettirir |
| **Hassasiyet** | Yüksek | Düşük |
| **Bağlam menüsü** | Sağ tık | Uzun basış |
| **İptal eylemi** | ESC tuşu | Kaydırarak uzaklaştırma, dışarı dokunma |

### Dokunmatik Geri Bildirim Gereksinimleri

```
Dokunma → Anında görsel değişiklik (< 50ms)
├── Vurgu durumu (arka plan rengi değişimi)
├── Hafifçe küçülme (scale down 0.95-0.98)
├── Dalgalanma efekti (Android Material Ripple)
├── Onay için haptik (titreşim) geri bildirimi
└── Asla yanıtsız bırakma!

Yükleme → 100ms içinde göster
├── Eylem > 100ms sürüyorsa
├── Spinner/ilerleme çubuğu göster
├── Butonu devre dışı bırak (çift dokunmayı önle)
└── Mümkünse iyimser (optimistic) UI kullan
```

### "Şişman Parmak" Sorunu

```
Sorun: Dokunma sırasında parmak hedefi kapatır
├── Kullanıcı tam olarak nereye dokunduğunu göremez
├── Görsel geri bildirim parmağın ALTINDA kalır
└── Hata oranını artırır

Çözümler:
├── Geri bildirimi dokunma noktasının ÜSTÜNDE göster (tooltip gibi)
├── Hassas görevler için imleç benzeri kaydırma (offset) kullan
├── Metin seçimi için büyütme büyüteci (loupe) kullan
├── Hedefleri hassasiyet gerektirmeyecek kadar büyük yap
```

---

## 4. Jest (Gesture) Psikolojisi

### Jest Keşfedilebilirliği Sorunu

```
Sorun: Jestler GÖRÜNMEZDİR.
├── Kullanıcı onları keşfetmeli/hatırlamalıdır
├── Hover/görsel ipucu yoktur
├── Dokunmadan farklı bir zihinsel modeldir
└── Birçok kullanıcı jestleri asla keşfedemez

Çözüm: Her zaman görünür bir alternatif sunun
├── Silmek için kaydır → Ayrıca sil butonu veya menüsü göster
├── Yenilemek için çek → Ayrıca yenile butonu göster
├── Yakınlaştırmak için çimdikle → Ayrıca yakınlaştırma kontrolleri göster
└── Jestleri tek yol değil, birer kısayol olarak kullanın
```

### Yaygın Jest Kuralları

| Jest | Evrensel Anlam | Kullanım |
|---------|-------------------|-------|
| **Dokunma** | Seç, etkinleştir | Birincil eylem |
| **Çift dokunma** | Yakınlaştır, beğen/favori | Hızlı eylem |
| **Uzun basış** | Bağlam menüsü, seçim modu | İkincil seçenekler |
| **Yatay kaydırma** | Navigasyon, silme, eylemler | Liste eylemleri |
| **Aşağı kaydırma** | Yenile, kapat | Çek-yenile |
| **Çimdikleme** | Yakınlaştır/Uzaklaştır | Haritalar, görseller |
| **İki parmak kaydırma**| Kaydırma içinde kaydırma | İçe içe kaydırmalar |

### Jest Belirginliği (Affordance) Tasarımı

```
Kaydırma eylemleri görsel ipuçlarına ihtiyaç duyar:

┌─────────────────────────────────────────┐
│  ┌───┐                                  │
│  │ ≡ │  Gizli eylemleri olan öğe...   → │ ← Kenar ipucu (kısmi renk)
│  └───┘                                  │
└─────────────────────────────────────────┘

✅ İyi: Kenarda hafif bir renk görünmesi kaydırmayı çağrıştırır
✅ İyi: Taşıma ikonu ( ≡ ) yeniden sıralamayı çağrıştırır
✅ İyi: Jesti açıklayan tanıtım ipucu (onboarding tooltip)
❌ Kötü: Görsel ipucu olmayan gizli jestler
```

---

## 5. Haptik Geri Bildirim Desenleri

### Haptik Neden Önemlidir?

```
Haptik şunları sağlar:
├── Bakmadan onay alma
├── Daha zengin, daha premium bir his
├── Erişilebilirlik (görme engelli kullanıcılar)
├── Azaltılmış hata oranı
└── Duygusal tatmin

Haptik olmadan:
├── "Ucuz" veya web sitesi gibi hissettirir
├── Kullanıcı eylemin algılanıp algılanmadığından emin olamaz
└── Keyif alma fırsatı kaçırılır
```

### iOS Haptik Türleri

| Tür | Yoğunluk | Kullanım Durumu |
|------|-----------|----------|
| `selection` | Hafif | Seçici kaydırma, anahtar, seçim |
| `light` | Hafif | Küçük eylemler, hover karşılığı |
| `medium` | Orta | Standart dokunma onayı |
| `heavy` | Güçlü | Önemli tamamlama, bırakma |
| `success` | Desen | Görev başarıyla tamamlandı |
| `warning` | Desen | Uyarı, dikkat gerekiyor |
| `error` | Desen | Hata oluştu |

### Android Haptik Türleri

| Tür | Kullanım Durumu |
|------|----------|
| `CLICK` | Standart dokunma geri bildirimi |
| `HEAVY_CLICK` | Önemli eylemler |
| `DOUBLE_CLICK` | Eylemleri onaylama |
| `TICK` | Kaydırma/tarama geri bildirimi |
| `LONG_PRESS` | Uzun basış etkinleştirme |
| `REJECT` | Hata/geçersiz eylem |

---

## 6. Mobil Bilişsel Yük

### Mobilin Masaüstünden Farkı

| Faktör | Masaüstü | Mobil | Etki |
|--------|---------|--------|-------------|
| **Dikkat** | Odaklanmış oturumlar | Sürekli kesinti | Mikro-oturumlar için tasarla |
| **Bağlam** | Kontrollü ortam | Her yer, her koşul | Kötü ışık, gürültü ile baş et |
| **Çoklu Görev** | Çoklu pencere | Tek uygulama görünür | Görevi uygulama içinde tamamla |
| **Giriş Hızı** | Hızlı (klavye) | Yavaş (dokunmatik) | Girişi minimize et, akıllı varsayılanlar |
| **Hata Kurtarma** | Kolay (geri al) | Daha zor | Hataları önle, kolay kurtarma sağla |

### Mobil Bilişsel Yükü Azaltma

```
1. Ekran başına TEK BİRİNCİL EYLEM
   └── Sırada ne yapılacağı net olsun
   
2. KADEMELİ AÇIKLAMA (Progressive Disclosure)
   └── Sadece şu an gerekeni göster
   
3. AKILLI VARSAYILANLAR
   └── Doldurulabilecekleri önceden doldur
   
4. GRUPLANDIRMA (Chunking)
   └── Uzun formları adımlara böl
   
5. HATIRLAMA YERİNE TANIMA (Recognition over Recall)
   └── Seçenekleri göster, kullanıcıyı hatırlamaya zorlama
   
6. BAĞLAM KALICILIĞI
   └── Kesinti veya arka plana geçişte durumu kaydet
```

### Mobil İçin Miller Yasası

```
Masaüstü: Çalışma belleğinde 7±2 öğe
Mobil: 5±1'e düşürün (daha fazla dikkat dağıtıcı)

Navigasyon: Maksimum 5 tab bar öğesi
Seçenekler: Menü seviyesi başına maksimum 5 öğe
Adımlar: İlerlemede görünür maksimum 5 adım
```

---

## 7. Dokunmatik Erişilebilirlik

### Motor Engeli Değerlendirmeleri

```
Motor engeli olan kullanıcılar:
├── Titremeleri olabilir (daha büyük hedeflere ihtiyaç duyarlar)
├── Yardımcı cihazlar kullanabilirler (farklı giriş yöntemi)
├── Sınırlı erişimleri olabilir (tek el zorunluluğu)
├── Daha fazla zamana ihtiyaç duyabilirler (zaman aşımlarından kaçının)
└── Yanlışlıkla dokunabilirler (onay gereksinimi)

Tasarım yanıtları:
├── Cömert dokunmatik hedefler (48dp+)
├── Jestler için ayarlanabilir zamanlama
├── Yıkıcı eylemler için geri alma (undo)
├── Anahtar kontrolü (switch control) desteği
└── Sesli kontrol desteği
```

---

## 8. Dokunmatik Hissiyatı ve Duygu

### Premium Hissiyat

```
Dokunmayı "premium" hissettiren nedir:
├── Anında yanıt (< 50ms)
├── Uygun haptik geri bildirimi
├── Pürüzsüz 60fps animasyonlar
├── Doğru direnç/fizik kuralları
├── Sesli geri bildirim (uygun olduğunda)
└── Yay (spring) fiziğine gösterilen özen
```

### Duygusal Dokunma Geri Bildirimi

| Duygu | Dokunma Yanıtı |
|---------|----------------|
| Başarı | Haptik başarı + konfeti/onay işareti |
| Hata | Haptik hata + sallanma (shake) animasyonu |
| Uyarı | Haptik uyarı + dikkat rengi |
| Keyif | Beklenmedik pürüzsüz animasyon |
| Güç | Önemli eylemde güçlü haptik |

---

## 9. Dokunmatik Psikolojisi Kontrol Listesi

### Her Ekrandan Önce

- [ ] **Tüm dokunmatik hedefler ≥ 44-48px mi?**
- [ ] **Birincil CTA başparmak bölgesinde mi?**
- [ ] **Yıkıcı eylemler onay gerektiriyor mu?**
- [ ] **Jest alternatifleri (görünür butonlar) var mı?**
- [ ] **Önemli eylemlerde haptik geri bildirimi var mı?**
- [ ] **Dokunmada anında görsel geri bildirim var mı?**
- [ ] **100ms'den uzun süren eylemler için yükleme durumları var mı?**

---

## 10. Hızlı Referans Kartı

### Dokunmatik Hedef Boyutları

```
                     iOS        Android     WCAG
Minimum:           44pt       48dp       44px
Önerilen:          48pt+      56dp+      -
Boşluklar:         8pt+       8dp+       8px+
```

### Başparmak Bölgesi Eylemleri

```
ÜST:      Navigasyon, ayarlar, geri (nadir kullanım)
ORTA:     İçerik, ikincil eylemler
ALT:      Birincil CTA, tab bar, FAB (sık kullanım)
```

---

> **Unutma:** Her dokunuş, kullanıcı ile cihaz arasında bir sohbetidir. Bunun hassas imleç noktaları gibi değil; doğal, duyarlı ve insan parmaklarına saygılı hissettirmesini sağlayın.
