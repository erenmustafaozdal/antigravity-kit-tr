---
name: frontend-design
description: Web arayüzü (UI) için tasarım odaklı düşünme ve karar verme. Bileşenler, düzenler, renk şemaları, tipografi tasarlarken veya estetik arayüzler oluştururken kullanın. Sabit değerleri değil, prensipleri öğretir.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Frontend Tasarım Sistemi

> **Felsefe:** Her pikselin bir amacı vardır. Ölçülü olmak lükstür. Kararları kullanıcı psikolojisi belirler.
> **Temel Prensip:** Ezberleme, DÜŞÜN. Varsayma, SOR.

---

## 🎯 Seçici Okuma Kuralı (ZORUNLU)

**GEREKLİ dosyaları her zaman, OPSİYONEL olanları sadece ihtiyaç duyduğunuzda okuyun:**

| Dosya | Durum | Ne Zaman Okunmalı? |
|------|--------|--------------|
| [ux-psychology.md](ux-psychology.md) | 🔴 **GEREKLİ** | Her zaman ilk önce okuyun! |
| [color-system.md](color-system.md) | ⚪ Opsiyonel | Renk/palet kararlarında |
| [typography-system.md](typography-system.md) | ⚪ Opsiyonel | Yazı tipi seçimi/eşleştirmelerinde |
| [visual-effects.md](visual-effects.md) | ⚪ Opsiyonel | Glassmorphism, gölgeler, gradyanlar |
| [animation-guide.md](animation-guide.md) | ⚪ Opsiyonel | Animasyon gerektiğinde |
| [motion-graphics.md](motion-graphics.md) | ⚪ Opsiyonel | Lottie, GSAP, 3B (3D) içeriklerde |
| [decision-trees.md](decision-trees.md) | ⚪ Opsiyonel | Bağlama özel şablonlarda |

> 🔴 **ux-psychology.md = HER ZAMAN OKUYUN. Diğerleri = Sadece ilgiliyse.**

---

## 🔧 Çalışma Zamanı Scriptleri (Runtime Scripts)

**Denetimler için bunları çalıştırın (okumayın, sadece çalıştırın):**

| Script | Amacı | Kullanım |
|--------|---------|-------|
| `scripts/ux_audit.py` | UX Psikolojisi ve Erişilebilirlik Denetimi | `python scripts/ux_audit.py <proje_yolu>` |

---

## ⚠️ KRİTİK: VARSAYMADAN ÖNCE SORUN (ZORUNLU)

> **DUR! Eğer kullanıcının isteği ucu açıksa, varsayılan olarak favori tercihlerinize yönelmeyin.**

### Kullanıcı Talebi Belirsizse Şunları SORUN:

**Renk belirtilmemiş mi?** Sorun:
> "Hangi renk paletini tercih edersiniz? (mavi/yeşil/turuncu/nötr/diğer?)"

**Stil belirtilmemiş mi?** Sorun: 
> "Nasıl bir stil hedefliyorsunuz? (minimal/cesur/retro/fütüristik/organik?)"

**Düzen (Layout) belirtilmemiş mi?** Sorun:
> "Bir düzen tercihiniz var mı? (tek sütun/ızgara/asimetrik/tam genişlik?)"

### ⛔ KAÇINILMASI GEREKEN VARSAYILAN EĞİLİMLER:

| YZ Varsayılan Eğilimi | Neden Kötü? | Yerine Ne Düşünülmeli? |
|---------------------|--------------|---------------|
| **Bento Izgaralar (Modern Klişe)** | Neredeyse her YZ tasarımında kullanılıyor | Bu içeriğin NEDEN bir ızgaraya ihtiyacı var? |
| **Hero Bölünmesi (Sol/Sağ)** | Tahmin edilebilir ve sıkıcı | Devasa tipografi veya dikey anlatıma ne dersiniz? |
| **Mesh/Aurora Gradyanlar** | "Yeni" tembel arka plan tercihi | Radikal bir renk eşleşmesi ne olabilir? |
| **Glassmorphism** | YZ'nin "premium" anlayışı | Katı, yüksek kontrastlı düz (flat) tasarıma ne dersiniz? |
| **Koyu Turkuaz / Finans Mavisi** | Mor yasağından kaçış noktası | Neden Kırmızı, Siyah veya Neon Yeşil değil? |
| **"Orchestrate / Empower" vb.** | YZ üretimi metin yazarlığı (copywriting) | Bir insan bunu nasıl söylerdi? |
| Karanlık arka plan + neon ışıltı | Aşırı kullanılmış, "YZ görünümü" | MARKANIN gerçekte neye ihtiyacı var? |
| **Her şeyi yuvarlamak** | Jenerik/Güvenli | Keskin, brütalist kenarları nerede kullanabilirim? |

> 🔴 **"Seçtiğiniz her 'güvenli' yapı sizi sıradan bir şablona bir adım daha yaklaştırır. RİSK ALIN."**

---

## 1. Kısıt Analizi (HER ZAMAN İLK ADIM)

Herhangi bir tasarım işinden önce bunlara CEVAP VERİN veya KULLANICIYA SORUN:

| Kısıt | Soru | Neden Önemli? |
|------------|----------|----------------|
| **Zaman Çizelgesi** | Ne kadar vaktimiz var? | Karmaşıklığı belirler |
| **İçerik** | Hazır mı yoksa yer tutucu mu? | Düzen esnekliğini etkiler |
| **Marka** | Mevcut rehberler var mı? | Renk/font seçimini belirleyebilir |
| **Teknoloji** | Hangi stack kullanılacak? | Yetenekleri etkiler |
| **Hedef Kitle** | Tam olarak kimler? | Tüm görsel kararları yönlendirir |

### Hedef Kitle → Tasarım Yaklaşımı

| Hedef Kitle | Ne Düşünülmeli? |
|----------|-------------|
| **Z Kuşağı** | Cesur, hızlı, mobil öncelikli, otantik |
| **Y Kuşağı** | Temiz, minimal, değer odaklı |
| **X Kuşağı** | Tanıdık, güvenilir, net |
| **Baby Boomer'lar** | Okunaklı, yüksek kontrastlı, basit |
| **B2B** | Profesyonel, veri odaklı, güven veren |
| **Lüks** | Ölçülü zarafet, geniş beyaz alanlar (whitespace) |

---

## 2. UX Psikolojisi Prensipleri

### Temel Yasalar (Bunları İçselleştirin)

| Yasa | Prensip | Uygulama |
|-----|-----------|-------------|
| **Hick Yasası** | Daha fazla seçenek = daha yavaş karar | Seçenekleri sınırlayın, kademeli açıklama kullanın |
| **Fitts Yasası** | Büyük + yakın = tıklaması daha kolay | CTA'leri (eylem düğmeleri) uygun boyutta yapın |
| **Miller Yasası** | Çalışma belleğinde ~7 öğe tutulabilir | İçeriği gruplara bölün (chunking) |
| **Von Restorff** | Farklı olan = akılda kalıcı | CTA'leri görsel olarak ayırt edici yapın |
| **Seri Konum** | En çok ilk/son hatırlanır | Kritik bilgiyi başa veya sona koyun |

### Duygusal Tasarım Seviyeleri

```
VİSERAL (Anlık)   → İlk izlenim: renkler, görseller, genel his
DAVRANIŞSAL (Kullanım) → Kullanım süreci: hız, geri bildirim, verimlilik
REFLEKTİF (Hafıza) → Sonrası: "Bunun benim hakkımda söylediklerini seviyorum"
```

### Güven İnşası

- Hassas işlemlerde güvenlik göstergeleri
- İlgili yerlerde sosyal kanıtlar (social proof)
- Net iletişim/destek erişimi
- Tutarlı, profesyonel tasarım
- Şeffaf politikalar

---

## 3. Düzen (Layout) Prensipleri

### Altın Oran (φ = 1.618)

```
Oransal uyum için kullanın:
├── İçerik : Yan Panel = Yaklaşık %62 : %38
├── Her başlık boyutu = Önceki × 1.618 (dramatik ölçek için)
├── Boşluklar şu sırayı takip edebilir: sm → md → lg (her biri × 1.618)
```

### 8-Piksel Izgara Mantığı

```
Tüm boşluk ve boyutlar 8'in katları olmalıdır:
├── Dar: 4px (mikro detaylar için yarım adım)
├── Küçük: 8px
├── Orta: 16px
├── Büyük: 24px, 32px
├── XL: 48px, 64px, 80px
└── İçerik yoğunluğuna göre ayarlayın
```

### Temel Boyutlandırma Prensipleri

| Öğe | Karar Kriteri |
|---------|---------------|
| **Dokunma Hedefleri**| Minimum rahat dokunma boyutu |
| **Butonlar** | Önem sıra hiyerarşisine göre yükseklik |
| **Input'lar** | Hizalama için buton yüksekliğiyle eşleştirme |
| **Kartlar** | Tutarlı ve nefes alan iç boşluk (padding) |
| **Okuma Genişliği** | En uygun 45-75 karakter arası |

---

## 4. Renk Prensipleri

### 60-30-10 Kuralı

```
%60 → Birincil/Arka Plan (sakin, nötr temel)
%30 → İkincil (destekleyici alanlar)
%10 → Vurgu (CTA'ler, önemli noktalar, dikkat çekici alanlar)
```

### Renk Psikolojisi (Karar Verme İçin)

| İhtiyacınız Olan... | Düşünülecek Tonlar | Kaçınılacaklar |
|----------------|---------------|-------|
| Güven, sakinlik | Mavi ailesi | Agresif kırmızılar |
| Büyüme, doğa | Yeşil ailesi | Endüstriyel griler |
| Enerji, aciliyet | Turuncu, kırmızı | Pasif maviler |
| Lüks, yaratıcılık | Koyu Turkuaz, Altın, Zümrüt | Ucuz hissettiren parlak renkler |
| Temiz, minimal | Nötr renkler | Boğucu ve aşırı renk kullanımı |

### Seçim Süreci

1. **Sektör nedir?** (seçenekleri daraltır)
2. **Hangi duygu hedefleniyor?** (birincil rengi belirler)
3. **Açık mı koyu mu mod?** (temeli atar)
4. Belirtilmemişse **KULLANICIYA SORUN**

Detaylı renk teorisi için: [color-system.md](color-system.md)

---

## 5. Tipografi Prensipleri

### Ölçek Seçimi

| İçerik Türü | Ölçek Oranı | His |
|--------------|-------------|------|
| Yoğun arayüz | 1.125-1.2 | Kompakt, verimli |
| Genel web | 1.25 | Dengeli (en yaygın) |
| Editöryel | 1.333 | Okunaklı, ferah |
| Hero/Ekran | 1.5-1.618 | Dramatik etki |

### Eşleştirme Mantığı

```
Kontrast + Uyum:
├── Hiyerarşi için yeterince FARKLI
├── Bütünlük için yeterince BENZER
└── Genellikle: ekran fontu + nötr font, veya serif + sans-serif
```

### Okunabilirlik Kuralları

- **Satır genişliği**: 45-75 karakter arası idealdir
- **Satır yüksekliği**: Gövde metni için 1.4-1.6 arası
- **Kontrast**: WCAG gereksinimlerini kontrol edin
- **Boyut**: Web'de gövde metni için 16px+

Detaylı tipografi için: [typography-system.md](typography-system.md)

---

## 6. Görsel Efekt Prensipleri

### Glassmorphism (Uygun Yerlerde)

```
Temel özellikler:
├── Yarı saydam arka plan
├── Arka plan bulanıklığı (backdrop blur)
├── Belirginlik için ince kenarlık (subtle border)
└── ⚠️ **UYARI:** Standart mavi/beyaz glassmorphism artık bir klişedir. Radikal bir şekilde kullanın veya hiç kullanmayın.
```

### Gölge Hiyerarşisi

```
Yükselti (Elevation) mantığı:
├── Daha üstteki öğeler = daha büyük gölgeler
├── Y-ekseni kayması > X-ekseni kayması (yukarıdan gelen ışık)
├── Çoklu katmanlar = daha gerçekçi görünüm
└── Karanlık mod: Gölge yerine parlama (glow) gerekebilir
```

### Gradyan Kullanımı

```
Uyumlu gradyanlar:
├── Renk çarkında komşu renkler (analogous)
├── VEYA aynı tonun farklı parlaklıkları
├── Keskin tamamlayıcı (complementary) çiftlerden kaçının
├── 🚫 **Mesh/Aurora Gradyanlara HAYIR** (yüzen lekeler)
└── Projeden projeye radikal bir şekilde DEĞİŞTİRİN
```

Detaylı efekt rehberi için: [visual-effects.md](visual-effects.md)

---

## 7. Animasyon Prensipleri

### Zamanlama Mantığı

```
Süre şunlara dayanır:
├── Mesafe (ne kadar uzaksa o kadar uzun)
├── Boyut (ne kadar büyükse o kadar yavaş)
├── Önem (kritikse o kadar net)
├── Bağlam (acilse hızlı, lüks ise yavaş)
```

### Easing (İvmelenme) Seçimi

| Eylem | Easing | Neden? |
|--------|--------|-----|
| Giriş | Ease-out | Yavaşla ve yerleş |
| Çıkış | Ease-in | Hızlan ve çık |
| Vurgu | Ease-in-out | Yumuşak ve bilinçli |
| Oyunbaz | Bounce | Eğlenceli, enerjik |

### Performans

- Sadece `transform` ve `opacity` değerlerini anime edin.
- Kullanıcının "hareketi azalt" (reduced-motion) tercihine saygı duyun.
- Düşük donanımlı cihazlarda test edin.

Animasyon desenleri için: [animation-guide.md](animation-guide.md), gelişmiş teknikler için: [motion-graphics.md](motion-graphics.md)

---

## 8. "Vay Canına" (Wow Factor) Kontrol Listesi

### Premium Göstergeler

- [ ] Cömert beyaz alan kullanımı (lükstür = nefes alma alanı)
- [ ] İnce derinlik ve boyutlandırma
- [ ] Yumuşak ve amaca hizmet eden animasyonlar
- [ ] Detaylara gösterilen özen (hizalama, tutarlılık)
- [ ] Bütünsel görsel ritim
- [ ] Özel (custom) öğeler (her şey varsayılan/default değil)

### Güven İnşası

- [ ] Uygun yerlerde güvenlik vurguları
- [ ] Sosyal kanıtlar / referanslar
- [ ] Net değer önerisi (unique value proposition)
- [ ] Profesyonel görseller
- [ ] Tutarlı tasarım dili

### Duygusal Tetikleyiciler

- [ ] İstenen duyguyu uyandıran Hero alanı
- [ ] İnsani öğeler (yüzler, hikayeler)
- [ ] İlerleme/başarı göstergeleri
- [ ] Keyif veren anlar (delight moments)

---

## 9. Anti-Desenler (YAPILMAMASI Gerekenler)

### ❌ Tembel Tasarım Göstergeleri

- Düşünülmeden kullanılan varsayılan sistem fontları
- Uyuşmayan hazır stok görseller
- Tutarsız boşluklar
- Birbiriyle yarışan çok fazla renk
- Hiyerarşisi olmayan metin yığınları
- Erişilebilir olmayan kontrast oranları

### ❌ YZ Eğilim Desenleri (KAÇININ!)

- **Her projede aynı renkler**
- **Varsayılan olarak karanlık + neon kombinasyonu**
- **Her şeyi mor/menekşe yapmak (MOR YASAĞI ✅)**
- **Basit açılış sayfaları için bile bento ızgaralar**
- **Mesh Gradyanlar ve Parlama Efektleri**
- **Aynı düzen yapısı / Vercel klonları**
- **Kullanıcı tercihlerini sormamak**

### ❌ Karanlık Desenler (Etik Dışı)

- Gizli maliyetler
- Sahte aciliyet oluşturma
- Zorlanmış eylemler
- Aldatıcı arayüzler
- Kullanıcıyı utandıran onaylama metinleri (confirmshaming)

---

## 10. Karar Süreci Özeti

```
HER tasarım görevi için:

1. KISITLAR
   └── Zaman çizelgesi, marka, teknoloji, kitle nedir?
   └── Belirsizse → SORUN

2. İÇERİK
   └── Hangi içerikler var?
   └── Hiyerarşi nasıl olmalı?

3. STİL YÖNÜ
   └── Bağlama ne uygun?
   └── Belirsizse → SORUN (varsayılan tercihinize yönelmeyin!)

4. UYGULAMA
   └── Yukarıdaki prensipleri uygulayın
   └── Anti-desenleri kontrol edin

5. İNCELEME
   └── "Bu kullanıcıya hizmet ediyor mu?"
   └── "Varsayılan tercihlerimden farklı mı?"
   └── "Bununla gurur duyar mıydım?"
```

---

## Referans Dosyalar

Belirli alanlarda daha derinlemesine rehberlik için:

- [color-system.md](color-system.md) - Renk teorisi ve seçim süreci
- [typography-system.md](typography-system.md) - Font eşleştirme ve ölçek kararları
- [visual-effects.md](visual-effects.md) - Efekt prensipleri ve teknikleri
- [animation-guide.md](animation-guide.md) - Hareketli tasarım prensipleri
- [motion-graphics.md](motion-graphics.md) - Gelişmiş: Lottie, GSAP, SVG, 3B, Parçacıklar
- [decision-trees.md](decision-trees.md) - Bağlama özel şablonlar
- [ux-psychology.md](ux-psychology.md) - Kullanıcı psikolojisi detayları

---

## İlgili Yetenekler

| Yetenek | Ne Zaman Kullanılır |
|-------|-------------|
| **frontend-design** (bu) | Kodlamadan ÖNCE - Tasarım prensiplerini öğrenin (renk, tipografi, UX psikolojisi) |
| **[web-design-guidelines](../web-design-guidelines/SKILL.md)** | Kodlamadan SONRA - Erişilebilirlik, performans ve en iyi pratikler için denetleyin |

## Tasarım Sonrası İş Akışı

Tasarımınızı uyguladıktan sonra denetimi çalıştırın:

```
1. TASARIM   → frontend-design prensiplerini okuyun ← ŞU AN BURADASINIZ
2. KOD       → Tasarımı uygulayın
3. DENETİM   → web-design-guidelines incelemesini çalıştırın
4. DÜZELTME  → Denetim sonuçlarını adresleyin
```

> **Sonraki Adım:** Kodlamadan sonra, erişilebilirlik, odak durumları (focus states), animasyonlar ve performans sorunları için uygulamanızı denetlemek üzere `web-design-guidelines` yeteneğini kullanın.

---

> **Unutmayın:** Tasarım, kopyalamak değil DÜŞÜNMEKTİR. Her proje, kendi benzersiz bağlamına ve kullanıcılarına göre taze bir değerlendirmeyi hak eder. **Sıradan SaaS Tasarımlarından Kaçının!**
