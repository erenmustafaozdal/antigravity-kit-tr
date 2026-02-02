# Görsel Efektler Referansı

> Modern CSS efekt prensipleri ve teknikleri - kavramları öğrenin, kendi varyasyonlarınızı yaratın.
> **Kopyalanacak sabit değerler yok - desenleri anlayın.**

---

## 1. Glassmorphism (Cam Morfizmi) Prensipleri

### Glassmorphism'i Başarılı Kılan Nedir?

```
Temel Özellikler:
├── Yarı saydam arka plan (düz renk yerine)
├── Arka plan bulanıklığı (backdrop-filter) (buzlu cam efekti)
├── Hafif kenarlık (border) (tanımlayıcı hatlar için)
└── Genellikle: Derinlik için hafif bir gölge
```

### Tasarım Deseni (Değerleri Özelleştirin)

```css
.glass {
  /* Saydamlık: İçerik okunabilirliğine göre opaklığı ayarlayın */
  background: rgba(R, G, B, OPAKLIK);
  /* OPAKLIK: Koyu arkaplanda 0.1-0.3, açık arkaplanda 0.5-0.8 */
  
  /* Bulanıklık (Blur): Artırdıkça "buzlanma" hissi artar */
  backdrop-filter: blur(MİKTAR);
  /* MİKTAR: 8-12px hafif, 16-24px güçlü etki */
  
  /* Kenarlık: Kenarları belirginleştirir */
  border: 1px solid rgba(255, 255, 255, OPAKLIK);
  /* OPAKLIK: Genellikle 0.1-0.3 arası */
  
  /* Köşe Yarıçapı: Tasarım sisteminize uygun olanı seçin */
  border-radius: YARIÇAPINIZ;
}
```

### Glassmorphism Ne Zaman Kullanılır?
- ✅ Renkli/Görsel arka planların üzerinde
- ✅ Modallar, katmanlar ve kartlar
- ✅ Arkasından içerik akan navigasyon çubukları
- ❌ Metin yoğunluğu fazla olan içerikler (okunabilirlik sorunları)
- ❌ Basit, düz renkli arka planlar (gereksizdir)

### Ne Zaman Kullanılmamalı?
- Düşük kontrastlı durumlar
- Erişilebilirliğin kritik olduğu içerikler
- Donanım performansı kısıtlı cihazlar

---

## 2. Neomorphism (Yeni Morfizm) Prensipleri

### Neomorphism'i Başarılı Kılan Nedir?

```
Temel Kavram: ÇİFT gölge kullanarak yumuşak, yüzeyden fırlamış öğeler
├── Işık gölgesi (ışık kaynağının yönünden gelen)
├── Karanlık gölge (zıt yönden gelen)
└── Arka planın çevreyle aynı olması (aynı renk)
```

### Tasarım Deseni

```css
.neo-raised {
  /* Arkaplan ebeveyn öğe ile AYNI OLMALIDIR */
  background: EBEVEYN_İLE_AYNI;
  
  /* İki gölge: Işık yönü + Karanlık yön */
  box-shadow: 
    MESAFE MESAFE BLUR rgba(isik-rengi),
    -MESAFE -MESAFE BLUR rgba(karanlik-rengi);
  
  /* MESAFE (Offset): Genellikle 6-12px */
  /* BLUR (Bulanıklık): Genellikle 12-20px */
}

.neo-pressed {
  /* Inset özelliği "içe basılmış" efekti yaratır */
  box-shadow: 
    inset MESAFE MESAFE BLUR rgba(karanlik-rengi),
    inset -MESAFE -MESAFE BLUR rgba(isik-rengi);
}
```

### Erişilebilirlik Uyarısı
⚠️ **Düşük kontrast** - idareli kullanın ve net sınırlar olduğundan emin olun.

### Ne Zaman Kullanılır?
- Dekoratif öğeler
- Hafif etkileşimli durumlar
- Düz renkli minimalist arayüzler

---

## 3. Gölge Hiyerarşisi (Shadow Hierarchy) Prensipleri

### Kavram: Gölgeler Yükseklik Belirtir

```
Daha yüksek seviye = Daha büyük gölge
├── Seviye 0: Gölge yok (yüzeyle bitişik)
├── Seviye 1: Hafif gölge (hafifçe kalkık)
├── Seviye 2: Orta gölge (kartlar, butonlar)
├── Seviye 3: Büyük gölge (modallar, dropdownlar)
└── Seviye 4: Derin gölge (havada asılı duran öğeler)
```

### Ayarlanacak Gölge Özellikleri

```css
box-shadow: OFFSET-X OFFSET-Y BLUR SPREAD RENK;

/* Offset: Gölgenin yönü */
/* Blur: Yumuşaklık (büyüdükçe yumuşar) */
/* Spread: Gölgenin yayılımı */
/* Renk: Genellikle düşük opaklıklı siyah */
```

### Doğal Gölgeler İçin Prensipler

1. **Y-offset değeri X'ten büyük olmalı** (ışık yukarıdan geliyormuş gibi).
2. **Düşük opaklık** (hafif etki için %5-15, belirgin etki için %15-25).
3. **Gerçekçilik için çoklu katman** (ortam ışığı + doğrudan ışık).
4. **Blur, mesafeyle (offset) orantılı artmalı** (daha uzak = daha bulanık).

### Karanlık Mod (Dark Mode) Gölgeleri
- Gölgeler karanlık arkaplanlarda daha az görünür.
- Opaklığı artırmak gerekebilir.
- Veya gölge yerine dış ışıma (glow/highlight) kullanılabilir.

---

## 4. Gradyan (Gradient) Prensipleri

### Türler ve Kullanım Alanları

| Tür | Desen | Kullanım Durumu |
|------|---------|----------|
| **Doğrusal (Linear)**| Bir hat boyunca A → B rengi | Arkaplanlar, butonlar, header'lar |
| **Radyal (Radial)** | Merkezden dışa doğru | Odak noktaları, spot ışıkları |
| **Konik (Conic)** | Merkez etrafında dönüş | Pasta grafikleri, yaratıcı efektler |

### Uyumlu Gradyanlar Oluşturma

```
İyi Gradyan Kuralları:
├── Renk çarkında BİRBİRİNE YAKIN renkleri seçin (analogous)
├── Veya aynı rengin farklı parlaklık seviyelerini kullanın
├── Zıt (complementary) renklerden kaçının (sert görünebilir)
└── Daha yumuşak geçişler için ara duraklar (middle stops) ekleyin
```

### Gradyan Sözdizimi Deseni

```css
.gradient {
  background: linear-gradient(
    YON,                 /* açı veya anahtar kelime (to right vb.) */
    RENK-DURAGI-1,       /* renk + isteğe bağlı konum */
    RENK-DURAGI-2,
    /* ... daha fazla durak */
  );
}

/* YON örnekleri: */
/* 90deg, 135deg, to right, to bottom right */
```

### Mesh Gradyanlar (Ağ Gradyanları)

```
Üst üste binen çoklu radyal gradyanlar:
├── Her biri farklı konumda
├── Her biri şeffaf geçişli (falloff)
├── **Hero bölümlerinde "Vay Canına" etkisi için ŞARTTIR**
└── Organik ve renkli bir efekt yaratır (Arama terimi: "Aurora Gradient CSS")
```

---

## 5. Kenarlık Efektleri (Border Effects) Prensipleri

### Gradyan Kenarlıklar

```
Teknik: Gradyan arka planlı pseudo-element
├── Ana öğenin padding değeri = kenarlık genişliği
├── Pseudo-element gradyan ile doldurulur
└── Maske veya clip ile kenarlık efekti oluşturulur
```

### Animasyonlu Kenarlıklar

```
Teknik: Dönen gradyan veya konik süpürme (sweep)
├── Pseudo-element içerikten daha büyük yapılır
├── Animasyon gradyanı döndürür
└── Overflow:hidden ile şekle göre kırpılır
```

### Işıyan Kenarlıklar (Glow Borders)

```css
/* Çoklu box-shadow ile dış ışıma yaratma */
box-shadow:
  0 0 KUCUK-BLUR RENK,
  0 0 ORTA-BLUR RENK,
  0 0 BUYUK-BLUR RENK;

/* Her katman ışımaya derinlik ekler */
```

---

## 6. Dış Işıma (Glow) Efekti Prensipleri

### Metin Işıması (Text Glow)

```css
text-shadow: 
  0 0 BLUR-1 RENK,
  0 0 BLUR-2 RENK,
  0 0 BLUR-3 RENK;

/* Çoklu katman = daha güçlü ışıma */
/* Büyük blur = daha yumuşak yayılım */
```

### Öğe Işıması (Element Glow)

```css
box-shadow:
  0 0 BLUR-1 RENK,
  0 0 BLUR-2 RENK;

/* Gerçekçi ışıma için öğenin rengiyle eşleştirin */
/* Hafif etki için düşük, neon etkisi için yüksek opaklık */
```

### Nabız Gibi Atan (Pulsing) Işıma Animasyonu

```css
@keyframes glow-pulse {
  0%, 100% { box-shadow: 0 0 KUCUK-BLUR RENK; }
  50% { box-shadow: 0 0 BUYUK-BLUR RENK; }
}

/* Easing ve süre (duration) hissi etkiler */
```

---

## 7. Katman (Overlay) Teknikleri

### Görseller Üzerinde Gradyan Katmanı

```
Amaç: Görseller üzerindeki metin okunabilirliğini artırmak
Desen: Şeffaftan opak renge doğru gradyan
Konum: Metnin görüneceği alan
```

```css
.overlay::after {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(
    YON,
    transparent YUZDE,
    rgba(0,0,0,OPAKLIK) 100%
  );
}
```

### Renkli Katman (Colored Overlay)

```css
/* Blend mode veya katmanlı gradyan */
background: 
  linear-gradient(OPAKLIK-ICEREN-RENGINIZ),
  url('gorsel.jpg');
```

---

## 8. Modern CSS Teknikleri

### Konteynır Sorguları (Container Queries)

```
Sadece viewport kesme noktaları yerine:
├── Bileşen KENDİ konteynırına tepki verir
├── Gerçekten modüler ve tekrar kullanılabilir bileşenler
└── Sözdizimi: @container (kosul) { }
```

### :has() Seçicisi (Selector)

```
Çocuk öğelere göre ebeveyn stilini belirleme:
├── "X çocuk öğesine sahip olan ebeveyn"
├── Eskiden imkansız olan desenleri mümkün kılar
└── Kademeli geliştirme (progressive enhancement) yaklaşımı
```

### Kaydırma Tetiklemeli Animasyonlar

```
Kaydırma ilerlemesine bağlı animasyonlar:
├── Kaydırma sırasında giriş/çıkış animasyonları
├── Parallax efektleri
├── İlerleme göstergeleri
└── Görünüm tabanlı veya kaydırma tabanlı zaman çizelgesi
```

---

## 9. Performans Prensipleri

### GPU Hızlandırmalı Özellikler

```
Anime etmesi KOLAY/UCUZ olanlar (GPU):
├── transform (translate, scale, rotate)
└── opacity

Anime etmesi ZOR/PAHALI olanlar (CPU - yeniden düzenleme tetikler):
├── width, height
├── top, left, right, bottom
├── margin, padding
└── box-shadow (her adımda yeniden hesaplanır)
```

### will-change Kullanımı

```css
/* İdareli kullanın, sadece ağır animasyonlar için */
.heavy-animation {
  will-change: transform;
}

/* Mümkünse animasyon bittikten sonra kaldırın */
```

### Hareketi Azaltma (Reduced Motion) Tercihi

```css
@media (prefers-reduced-motion: reduce) {
  /* Animasyonları kapatın veya minimuma indirin */
  /* Kullanıcı tercihine saygı duyun */
}
```

---

## 10. Efekt Seçimi Kontrol Listesi

Herhangi bir efekti uygulamadan önce:

- [ ] **Bir amaca hizmet ediyor mu?** (Sadece süs değil mi?)
- [ ] **Bağlama uygun mu?** (Marka, hedef kitle)
- [ ] **Önceki projelerden farklılaştınız mı?** (Tekrardan kaçının)
- [ ] **Erişilebilir mi?** (Kontrast, hareket hassasiyeti)
- [ ] **Performanslı mı?** (Özellikle mobilde)
- [ ] **Kullanıcı tercihini sordunuz mu?** (Stil ucu açıksa)

### Anti-Desenler (Yapılmaması Gerekenler)

- ❌ Her öğeye Glassmorphism uygulamak (kitsch görünüm)
- ❌ Varsayılan olarak hep "Karanlık + Neon" seçmek (tembel YZ görünümü)
- ❌ **Derinlik içermeyen statik/düz tasarımlar (BAŞARISIZLIK)**
- ❌ Okunabilirliğe zarar veren efektler
- ❌ Amacı olmayan animasyonlar

---

> **Unutmayın**: Efektler anlamı güçlendirmelidir. Sırf "havalı görünüyor" diye değil; amaç ve bağlama göre seçim yapın.
