# Animasyon Rehberi Referansı

> Animasyon prensipleri ve zamanlama psikolojisi - kopyalamayı değil, karar vermeyi öğrenin.
> **Ezberlenecek sabit süreler yok - zamanlamayı neyin etkilediğini anlayın.**

---

## 1. Süre (Duration) Prensipleri

### Zamanlamayı Neler Etkiler?

```
Animasyon hızını belirleyen faktörler:
├── MESAFE: Daha uzak mesafe = daha uzun süre
├── BOYUT: Daha büyük öğeler = daha yavaş animasyonlar
├── KARMAŞIKLIK: Karmaşık öğeler = işlemesi daha uzun sürer
├── ÖNEM: Kritik eylemler = net ve belirgin geri bildirim
└── BAĞLAM: Acil = hızlı, lüks/premium = yavaş
```

### Amaca Göre Süre Aralıkları

| Amaç | Aralık | Neden? |
|---------|-------|-----|
| Anlık geri bildirim | 50-100ms | Algı eşiğinin altında |
| Mikro-etkileşimler | 100-200ms | Hızlı ama fark edilebilir |
| Standart geçişler | 200-300ms | Rahat bir tempo |
| Karmaşık animasyonlar | 300-500ms | Takip etmek için gereken süre |
| Sayfa geçişleri | 400-600ms | Yumuşak bir devir teslim |
| **Etkileyici/Lüks Efektler** | 800ms+ | Dramatik, organik yay (spring) tabanlı, katmanlı |

### Süre Seçimi

Kendinize sorun:
1. Öğe ne kadar uzağa hareket ediyor?
2. Bu değişikliğin fark edilmesi ne kadar önemli?
3. Kullanıcı bekliyor mu yoksa bu bir arka plan işlemi mi?

---

## 2. Easing (İvmelenme) Prensipleri

### Easing Ne İşe Yarar?

```
Easing = hızın zamanla nasıl değiştiği
├── Linear (Doğrusal): Sabit hız (mekanik, robotik)
├── Ease-out: Hızlı başlar, yavaş biter (doğal giriş)
├── Ease-in: Yavaş başlar, hızlı biter (doğal çıkış)
└── Ease-in-out: Her iki uçta yavaş (yumuşak, bilinçli)
```

### Ne Zaman Hangisi Kullanılmalı?

| Easing | En İyi Kullanım | Hissi |
|--------|----------|------------|
| **Ease-out** | Giriş yapan öğeler | Varış, yerleşme |
| **Ease-in** | Çıkış yapan öğeler | Ayrılma, terk etme |
| **Ease-in-out** | Vurgu, döngüler | Bilinçli, yumuşak |
| **Linear** | Sürekli hareket | Mekanik, sabit |
| **Bounce/Elastic** | Oyunbaz arayüzler | Eğlenceli, enerjik |

### Temel Desen

```css
/* Görünüme giriş = ease-out (yavaşlama) */
.enter {
  animation-timing-function: ease-out;
}

/* Görünümden çıkış = ease-in (hızlanma) */
.exit {
  animation-timing-function: ease-in;
}

/* Sürekli hareket = ease-in-out */
.continuous {
  animation-timing-function: ease-in-out;
}
```

---

## 3. Mikro-Etkileşim (Micro-Interaction) Prensipleri

### İyi Bir Mikro-Etkileşimi Ne Oluşturur?

```
Mikro-etkileşimlerin amacı:
├── GERİ BİLDİRİM: Eylemin gerçekleştiğini onayla
├── REHBERLİK: Nelerin mümkün olduğunu göster
├── DURUM: Mevcut durumu belirt
└── KEYİF: Küçük mutluluk anları yarat
```

### Buton Durumları

```
Hover (Üzerine Gelme) → Hafif görsel değişiklik (yükselme, renk, ölçek)
Active (Basılma) → Basılma hissi (boyut küçültme, gölge değişimi)
Focus (Odak) → Net gösterge (kenarlık, halka)
Loading (Yükleniyor) → İlerleme göstergesi (spinner, skeleton)
Success (Başarı) → Onay (tik işareti, renk değişimi)
```

### Prensipler

1. **Hemen yanıt verin** (100ms algı eşiğinin altında)
2. **Eylemle eşleştirin** (basma = `scale(0.95)`, hover = `translateY(-4px) + parlama`)
3. **Cesur ama yumuşak olun** (Usta işi hissettir)
4. **Tutarlı olun** (ayni eylemler = aynı geri bildirim)

---

## 4. Yükleme Durumları (Loading States) Prensipleri

### Bağlama Göre Türler

| Durum | Yaklaşım |
|-----------|----------|
| Hızlı yükleme (<1sn) | Göstergeye gerek yok |
| Orta (1-3sn) | Spinner veya basit animasyon |
| Uzun (3sn+) | İlerleme çubuğu veya skeleton |
| Bilinmeyen süre | Belirsiz (indeterminate) gösterge |

### Skeleton Ekranlar

```
Amaç: Algılanan bekleme süresini azaltmak
├── Düzenin şeklini hemen göster
├── Hafifçe anime et (shimmer, nabız efekti)
├── Hazır olduğunda içerikle değiştir
└── Spinner'dan daha hızlı hissettirir
```

### İlerleme Göstergeleri

```
İlerleme ne zaman gösterilmeli:
├── Kullanıcı tarafından başlatılan eylemler
├── Dosya yükleme/indirme
├── Çok adımlı süreçler
└── Uzun süren operasyonlar

Ne zaman GEREKMEZ:
├── Çok hızlı işlemler
├── Arka plan görevleri
├── İlk sayfa yüklemeleri (skeleton daha iyidir)
```

---

## 5. Sayfa Geçişleri Prensipleri

### Geçiş Stratejisi

```
Basit kural: Hızlı çıkış, daha yavaş giriş
├── Giden içerik hızla kaybolur (fade)
├── Gelen içerik anime edilerek girer
└── "Her şeyin aynı anda hareket etmesi" karmaşasını önler
```

### Yaygın Desenler

| Desen | Ne Zaman Kullanılır |
|---------|-------------|
| **Fade** | Güvenli varsayılan, her yerde çalışır |
| **Slide (Kaydırma)** | Ardışık navigasyon (ileri/geri) |
| **Scale (Ölçek)** | Modalları açma/kapama |
| **Shared element (Paylaşılan öğe)** | Görsel sürekliliği sağlamak |

### Yön Eşleştirme

```
Navigasyon yönü = animasyon yönü
├── İleri → Sağdan kaydır
├── Geri → Soldan kaydır
├── Daha derine → Merkezden büyüt (scale up)
├── Geri yukarı → Küçült (scale down)
```

---

## 6. Kaydırma (Scroll) Animasyonu Prensipleri

### Kademeli Ortaya Çıkarma (Progressive Reveal)

```
Kullanıcı kaydırdıkça içerik belirir:
├── İlk bilişsel yükü azaltır
├── Keşfetmeyi ödüllendirir
├── Hantal hissettirmemelidir
└── Kapatma seçeneği sunulmalıdır (erişilebilirlik)
```

### Tetikleme Noktaları

| Ne Zaman Tetiklenmeli | Etkisi |
|-----------------|--------|
| Görüş alanına girer girmez | Standart açılma |
| Görüş alanında merkezlendiğinde | Vurgu için |
| Kısmen görünür olduğunda | Daha erken açılma |
| Tamamen görünür olduğunda | Geç tetikleme |

### Animasyon Özellikleri

- Opaklık artışı (fade in)
- Yukarı kaydırma (slide up - transform)
- Ölçeklendirme (scale - transform)
- Yukarıdakilerin kombinasyonu

### Performans

- Intersection Observer kullanın
- Sadece transform/opacity değerlerini anime edin
- Gerekiyorsa mobilde etkileri azaltın

---

## 7. Hover (Üzerine Gelme) Efektleri Prensipleri

### Efekti Eylemle Eşleştirme

| Öğe | Efekt | Amaç |
|---------|--------|--------|
| **Tıklanabilir kart** | Yükselme + gölge | "Bu etkileşimlidir" |
| **Buton** | Renk/parlaklık değişimi | "Bana bas" |
| **Görsel** | Zoom/ölçeklendirme | "Daha yakından bak" |
| **Link** | Alt çizgi/renk değişimi | "Buraya git" |

### Prensipler

1. **Etkileşimi sinyalleyin** - hover tıklanabilir olduğunu gösterir
2. **Aşırıya kaçmayın** - küçük değişiklikler yeterlidir
3. **Önem derecesini eşleştirin** - büyük değişiklik = daha önemli eylem
4. **Dokunmatik alternatifleri** - hover mobilde çalışmaz, bunu unutmayın

---

## 8. Geri Bildirim Animasyonu Prensipleri

### Başarı Durumları

```
Uygun şekilde kutlayın:
├── Küçük eylem → hafif bir onay/renk
├── Büyük eylem → daha belirgin animasyon
├── Tamamlama → tatmin edici animasyon
└── Marka kişiliğiyle eşleştirin
```

### Hata Durumları

```
Panik yaratmadan dikkat çekin:
├── Renk değişimi (semantik kırmızı)
├── Sarsıntı (shake) animasyonu (kısa!)
├── Hata alanına odaklanma (focus)
└── Net mesajlar
```

### Zamanlama

- Başarı: Biraz daha uzun (anın tadını çıkar)
- Hata: Hızlı (eylemi geciktirme)
- Yükleme: Tamamlanana kadar sürekli

---

## 9. Performans Prensipleri

### Anime Etmesi "Ucuz" (Kolay) Olanlar

```
GPU hızlandırmalı (HIZLI):
├── transform: translate, scale, rotate
└── opacity: 0'dan 1'e
```

### CPU Yoğunluklu (YAVAŞ) Olanlar

```
Sürekli yeniden hesaplama gerektirir:
├── width, height
├── top, left, right, bottom
├── margin, padding
├── border-radius değişiklikleri
└── box-shadow değişiklikleri
```

### Optimizasyon Stratejileri

1. Mümkün olduğunda **transform/opacity** kullanın
2. **Layout tetikleyicilerinden** (boyut/konum değişiklikleri) kaçının
3. **will-change** özelliğini idareli kullanın (tarayıcıya ipucu verir)
4. Sadece geliştirme makinesinde değil, **düşük donanımlı cihazlarda** da test edin

### Kullanıcı Tercihlerine Saygı

```css
@media (prefers-reduced-motion: reduce) {
  /* Bu tercihe saygı duyun */
  /* Sadece zorunlu animasyonları bırakın */
  /* Dekoratif hareketleri azaltın veya kaldırın */
}
```

---

## 10. Animasyon Karar Kontrol Listesi

Animasyon eklemeden önce:

- [ ] **Bir amacı var mı?** (geri bildirim/rehberlik/keyif)
- [ ] **Zamanlama uygun mu?** (çok hızlı veya çok yavaş değil mi?)
- [ ] **Doğru easing'i seçtiniz mi?** (giriş/çıkış/vurgu)
- [ ] **Performanslı mı?** (sadece transform/opacity mi kullanıyor?)
- [ ] **Hareketi azaltma tercihi test edildi mi?** (erişilebilirlik)
- [ ] **Diğer animasyonlarla tutarlı mı?** (aynı zamanlama hissi)
- [ ] **Varsayılan ayarlarınızın dışına çıktınız mı?** (çeşitlilik kontrolü)
- [ ] **Belirsizse kullanıcıya stil tercihini sordunuz mu?**

### Anti-Desenler (Yapılmaması Gerekenler)

- ❌ Her projede aynı zamanlama değerlerini kullanmak
- ❌ Sadece "animasyon olsun diye" animasyon yapmak
- ❌ Hareketi azaltma (reduced-motion) tercihini görmezden gelmek
- ❌ CPU yoğunluklu (pahalı) özellikleri anime etmek
- ❌ Aynı anda çok fazla şeyin anime edilmesi
- ❌ Kullanıcıyı yoran ve bekleten gecikmeler

---

> **Unutmayın**: Animasyon bir iletişim biçimidir. Her hareketin bir anlamı olmalı ve kullanıcı deneyimine hizmet etmelidir.
