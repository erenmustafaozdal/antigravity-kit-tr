# Renk Sistemi Referansı

> Renk teorisi prensipleri, seçim süreci ve karar verme yönergeleri.
> **Ezberlenecek hex kodları yok - renk hakkında DÜŞÜNMEYİ öğrenin.**

---

## 1. Renk Teorisi Temelleri

### Renk Çarkı

```
                    SARI
                      │
           Sarı-      │    Sarı-
           Yeşil      │    Turuncu
               ╲       │       ╱
                ╲      │      ╱
      YEŞİL ─────────── ● ─────────── TURUNCU
                ╱      │      ╲
               ╱       │       ╲
            Mavi-      │    Kırmızı-
            Yeşil      │    Turuncu
                       │
                    KIRMIZI
                       │
                     MOR
                    ╱       ╲
               Mavi-         Kırmızı-
                Mor            Mor
                    ╲       ╱
                      MAVİ
```

### Renk İlişkileri

| Şema | Nasıl Oluşturulur | Ne Zaman Kullanılır |
|--------|---------------|-------------|
| **Monokromatik** | TEK bir ton seçin, sadece parlaklık/doygunluğu değiştirin | Minimal, profesyonel, bütünsel |
| **Analog** | Çark üzerinde YAN YANA 2-3 ton seçin | Uyumlu, sakin, doğadan ilham alan |
| **Tamamlayıcı** | Çark üzerinde karsılıklı (ZIT) tonları seçin | Yüksek kontrastlı, canlı, dikkat çekici |
| **Split-Complementary** | Temel + tamamlayıcının yanındaki 2 renk | Dinamik ama dengeli |
| **Triadik** | Çark üzerinde EŞİT mesafedeki 3 ton | Canlı, oyunbaz, yaratıcı |

### Şema Nasıl Seçilir?
1. **Projenin ruh hali nedir?** Sakin → Analog. Cesur → Tamamlayıcı.
2. **Kaç renk gerekiyor?** Minimal → Monokromatik. Karmaşık → Triadik.
3. **Hedef kitle kim?** Muhafazakar → Monokromatik. Genç → Triadik.

---

## 2. 60-30-10 Kuralı

### Dağılım Prensibi
```
┌─────────────────────────────────────────────────┐
│                                                 │
│     %60 BİRİNCİL (Arka plan, geniş alanlar)     │
│     → Nötr veya sakinleştirici olmalı           │
│     → Genel tonu bu belirler                    │
│                                                 │
├────────────────────────────────────┬────────────┤
│                                    │            │
│   %30 İKİNCİL                      │ %10 VURGU  │
│   (Kartlar, bölümler, başlıklar)   │ (CTA'ler,  │
│   → Baskın olmadan destekler       │ detaylar)  │
│                                    │ → Dikkat   │
│                                    │   çeker    │
└────────────────────────────────────┴────────────┘
```

### Uygulama Deseni
```css
:root {
  /* %60 - Açık/koyu mod ve ruh haline göre seçin */
  --color-bg: /* beyaz, kirli beyaz veya koyu gri */
  --color-surface: /* arka plandan hafifçe farklı */
  
  /* %30 - Marka veya bağlama göre seçin */
  --color-secondary: /* birincil rengin soluk versiyonu veya nötr */
  
  /* %10 - İstenen eylem/duyguya göre seçin */
  --color-accent: /* canlı, dikkat çekici */
}
```

---

## 3. Renk Psikolojisi - Anlam ve Seçim

### Bağlama Göre Nasıl Seçilir?

| Proje Türü... | Şu Tonları Düşünün | Neden? |
|------------------|---------------------|-----|
| **Finans, Teknoloji, Sağlık** | Maviler, Turkuazlar | Güven, istikrar, sakinlik |
| **Eko, Wellness, Doğa** | Yeşiller, Toprak tonları | Büyüme, sağlık, organik |
| **Gıda, Enerji, Gençlik** | Turuncu, Sarı, Sıcak tonlar | İştah, heyecan, sıcaklık |
| **Lüks, Güzellik, Yaratıcılık** | Koyu Turkuaz, Altın, Siyah | Sofistike, premium |
| **Aciliyet, İndirim, Uyarı** | Kırmızı, Turuncu | Eylem, dikkat, tutku |

### Duygusal Çağrışımlar (Karar Verme İçin)

| Renk Ailesi | Olumlu Çağrışımlar | Dikkat Edilmesi Gerekenler |
|------------|----------------------|----------|
| **Mavi** | Güven, sakinlik, profesyonellik | Soğuk ve kurumsal hissettirebilir |
| **Yeşil** | Büyüme, doğa, başarı | Fazla kullanılırsa sıkıcı olabilir |
| **Kırmızı** | Tutku, aciliyet, enerji | Uyarıcıdır, idareli kullanın |
| **Turuncu** | Sıcaklık, dostça, yaratıcı | Doygunluğu fazlaysa ucuz hissettirebilir |
| **Mor** | ⚠️ **YASAKLI** - YZ bunu çok fazla kullanır! | Yerine Koyu Turkuaz/Bordo/Zümrüt kullanın |
| **Sarı** | İyimserlik, dikkat, mutluluk | Okuması zordur, vurgu olarak kullanın |
| **Siyah** | Zarafet, güç, modernlik | Ağır hissettirebilir |
| **Beyaz** | Temiz, minimal, açık | Steril/soğuk hissettirebilir |

### Seçim Süreci:
1. **Hangi sektör?** → 2-3 renk ailesine indirin.
2. **Hangi duygu?** → Ana rengi seçin.
3. **Hangi kontrast?** → Açık mı koyu mu mod olacağına karar verin.
4. **KULLANICIYA SORUN** → İlerlemeden önce onay alın.

---

## 4. Palet Üretme Prensipleri

### Tek Bir Renkten Üretme (HSL Yöntemi)

Hex kodlarını ezberlemek yerine **HSL değerlerini manipüle etmeyi** öğrenin:

```
HSL = Hue (Ton), Saturation (Doygunluk), Lightness (Parlaklık)

Hue (0-360): Renk ailesi
  0/360 = Kırmızı
  60 = Sarı
  120 = Yeşil
  180 = Turkuaz
  240 = Mavi
  300 = Mor

Saturation (0-100%): Rengin yoğunluğu
  Düşük = Soluk, sofistike
  Yüksek = Canlı, enerjik

Lightness (0-100%): Parlaklık
  0% = Siyah
  50% = Saf renk
  100% = Beyaz
```

### Tam Bir Palet Oluşturma

Seçilen herhangi bir temel rengi kullanarak bir ölçek oluşturun:

```
Parlaklık (Lightness) Ölçeği:
  50  (en açık) → L: 97%
  100           → L: 94%
  200           → L: 86%
  300           → L: 74%
  400           → L: 66%
  500 (temel)    → L: 50-60%
  600           → L: 48%
  700           → L: 38%
  800           → L: 30%
  900 (en koyu) → L: 20%
```

### Doygunluk Ayarları

| Bağlam | Doygunluk Seviyesi |
|---------|-----------------|
| **Profesyonel/Kurumsal** | Düşük (%40-60) |
| **Eğlenceli/Genç** | Yüksek (%70-90) |
| **Karanlık Mod** | %10-20 azaltın |
| **Erişilebilirlik** | Kontrastı kontrol edin, gerekirse ayarlayın |

---

## 5. Bağlama Göre Seçim Rehberi

### Palet Kopyalamak Yerine Şu Süreci İzleyin:

**Adım 1: Bağlamı Tanımlayın**
```
Proje türü nedir?
├── E-ticaret → Güven ve aciliyet dengesi gerekir
├── SaaS/Dashboard → Göz yormayan, veri odaklı yapı
├── Sağlık/Zindelik → Sakinleştirici, doğal his
├── Lüks/Premium → Gösterişsiz zarafet (understated elegance)
├── Yaratıcı/Portfolyo → Kişilik sahibi, akılda kalıcı
└── Diğer → Kullanıcıya SORUN
```

**Adım 2: Birincil Renk Ailesini Seçin**
```
Bağlama göre BİR tanesini seçin:
- Mavi ailesi (güven)
- Yeşil ailesi (büyüme)
- Sıcak renkler (enerji)
- Nötr renkler (zarif)
- VEYA kullanıcı tercihini sorun
```

**Adım 3: Açık/Koyu Moda Karar Verin**
```
Şunları düşünün:
- Kullanıcı tercihi?
- Sektör standartları?
- İçerik türü? (metin yoğunsa açık renk tercih edilir)
- Kullanım zamanı? (gece uygulaması = koyu seçenek)
```

**Adım 4: Prensipleri Kullanarak Palet Üretin**
- HSL manipülasyonu kullanın
- 60-30-10 kuralını izleyin
- Kontrastı kontrol edin (WCAG)
- Gerçek içerikle test edin

---

## 6. Karanlık Mod (Dark Mode) Prensipleri

### Temel Kurallar (Sabit Kod Yok)

1. **Asla saf siyah kullanmayın** → Çok koyu, hafif renk tonu içeren gri kullanın
2. **Asla saf beyaz metin kullanmayın** → %87-92 parlaklık seviyesini tercih edin
3. **Doygunluğu azaltın** → Canlı renkler karanlık modda gözü yorar
4. **Yükselti = Parlaklık** → Daha üstteki öğeler hafifçe daha açık olmalı

### Karanlık Modda Kontrast

```
Arka plan katmanları (yükselti arttıkça koyudan açığa doğru):
Katman 0 (temel)     → En koyu
Katman 1 (kartlar)   → Hafif daha açık
Katman 2 (modallar)  → Daha da açık
Katman 3 (popup'lar) → Karanlıktaki en açık gri
```

### Renklerin Karanlık Moda Uyarlanması

| Açık Mod | Karanlık Mod Ayarı |
|------------|---------------------|
| Yüksek doygunluklu vurgu | Doygunluğu %10-20 azaltın |
| Saf beyaz arka plan | Marka rengi sızdırılmış koyu gri |
| Siyah metin | Açık gri (saf beyaz değil) |
| Renkli arka planlar | Doygunluğu azaltılmış, daha koyu sürümler |

---

## 7. Erişilebilirlik Yönergeleri

### Kontrast Gereksinimleri (WCAG)

| Seviye | Normal Metin | Büyük Metin |
|-------|-------------|------------|
| AA (minimum) | 4.5:1 | 3:1 |
| AAA (gelişmiş) | 7:1 | 4.5:1 |

### Kontrast Nasıl Kontrol Edilir?

1. **Renkleri parlaklık (luminance) değerine çevirin**
2. **Oranı hesaplayın**: (daha açık + 0.05) / (daha koyu + 0.05)
3. **Oran gereksinimi karşılayana kadar ayarlayın**

### Güvenli Desenler

| Kullanım Durumu | Yönerge |
|----------|-----------|
| **Açık zeminde metin** | %35 veya daha az parlaklık kullanın |
| **Koyu zeminde metin** | %85 veya daha fazla parlaklık kullanın |
| **Beyaz üzerinde ana renk** | Yeterince koyu olduğundan emin olun |
| **Butonlar** | Arka plan ve metin arasında yüksek kontrast sağlayın |

---

## 8. Renk Seçimi Kontrol Listesi

Herhangi bir renk seçimini kesinleştirmeden önce doğrulayın:

- [ ] **Kullanıcı tercihi soruldu mu?** (belirtilmemişse)
- [ ] **Proje bağlamıyla uyuşuyor mu?** (sektör, kitle)
- [ ] **60-30-10 kuralına uyuluyor mu?** (dengeli dağılım)
- [ ] **WCAG uyumlu mu?** (kontrast kontrol edildi)
- [ ] **Her iki modda da çalışıyor mu?** (karanlık mod gerekiyorsa)
- [ ] **Varsayılan/favori tercihiniz mi?** (çeşitlilik kontrolü)
- [ ] **Son projenizden farklı mı?** (tekrarı önleyin)

---

## 9. Kaçınılması Gereken Anti-Desenler

### ❌ YAPMAYIN:
- Her projede aynı hex kodlarını kopyalamak
- Varsayılan olarak mor/menekşe tonlarına yönelmek (YZ eğilimi)
- Varsayılan olarak karanlık mod + neon kombinasyonunu seçmek (YZ eğilimi)
- Arka plan için saf siyah (#000000) kullanmak
- Karanlık modda saf beyaz (#FFFFFF) metin kullanmak
- Kullanıcının sektör bağlamını görmezden gelmek
- Kullanıcıya tercihlerini sormayı atlamak

### ✅ YAPIN:
- Her proje için sıfırdan palet üretin
- Kullanıcıya renk tercihlerini sorun
- Sektörü ve hedef kitleyi göz önünde bulundurun
- Esnek manipülasyon için HSL kullanın
- Kontrastı ve erişilebilirliği test edin
- Açık VE koyu seçenekler sunun

---

> **Unutmayın**: Renkler birer tercihtir, varsayılan değil. Her proje, kendi benzersiz bağlamına göre düşünülmüş bir seçimi hak eder.
