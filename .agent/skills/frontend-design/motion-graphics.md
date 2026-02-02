# Hareketli Grafikler (Motion Graphics) Referansı

> Premium web deneyimleri için gelişmiş animasyon teknikleri - Lottie, GSAP, SVG, 3B, Parçacıklar.
> **Prensipleri öğrenin, "Vay Canına" (WOW) efektleri yaratın.**

---

## 1. Lottie Animasyonları

### Lottie Nedir?

```
JSON tabanlı vektör animasyonlar:
├── After Effects'ten Bodymovin aracılığıyla dışa aktarılır
├── Hafiftir (GIF veya videodan daha küçüktür)
├── Ölçeklenebilirdir (vektör tabanlıdır, pikselleşme olmaz)
├── Etkileşimlidir (oynatma, bölümler kontrol edilebilir)
└── Çok platformludur (web, iOS, Android, React Native)
```

### Lottie Ne Zaman Kullanılır?

| Kullanım Durumu | Neden Lottie? |
|----------|-------------|
| **Yükleme (Loading) animasyonları** | Markaya özel, yumuşak, hafif |
| **Boş durum (Empty state) ekranları** | İlgi çekici illüstrasyonlar |
| **Onboarding akışları** | Karmaşık, çok adımlı animasyonlar |
| **Başarı/Hata geri bildirimi** | Keyifli mikro-etkileşimler |
| **Animasyonlu ikonlar** | Platformlar arası tutarlılık |

### Prensipler

- Performans için dosya boyutunu 100KB'ın altında tutun.
- Döngüleri (loop) idareli kullanın (dikkat dağıtmaktan kaçının).
- Hareketi azaltma (reduced-motion) tercihi için statik bir yedek (fallback) sunun.
- Mümkünse animasyon dosyalarını tembel yükleme (lazy load) ile getirin.

### Kaynaklar

- LottieFiles.com (ücretsiz kütüphane)
- After Effects + Bodymovin (özel tasarımlar)
- Figma eklentileri (tasarımdan dışa aktarma)

---

## 2. GSAP (GreenSock)

### GSAP'i Farklı Kılan Nedir?

```
Profesyonel, zaman çizelgesi (timeline) tabanlı animasyon:
├── Diziler üzerinde hassas kontrol
├── Kaydırma tabanlı animasyonlar için ScrollTrigger
├── Şekil geçişleri için MorphSVG
├── Fizik tabanlı easing seçenekleri
└── Herhangi bir DOM öğesiyle çalışır
```

### Temel Kavramlar

| Kavram | Amaç |
|---------|---------|
| **Tween** | Tekil A→B animasyonu |
| **Timeline** | Sıralı/üst üste binen animasyonlar |
| **ScrollTrigger** | Kaydırma konumu oynatmayı kontrol eder |
| **Stagger** | Öğeler arasında kademeli geçiş efekti |

### GSAP Ne Zaman Kullanılır?

- ✅ Karmaşık sıralı animasyonlar
- ✅ Kaydırma ile tetiklenen ortaya çıkma efektleri
- ✅ Hassas zamanlama kontrolü gerektiğinde
- ✅ SVG morphing (şekil değiştirme) efektleri
- ❌ Basit hover/focus efektleri (CSS kullanın)
- ❌ Performansın kritik olduğu mobil görünümler (daha ağırdır)

### Prensipler

- Orkestrasyon için zaman çizelgesi (timeline) kullanın (tekil tween'ler yerine).
- Kademeli gecikme (Stagger delay): Öğeler arasında 0.05-0.15sn arası.
- ScrollTrigger: Görüş alanına girişin %70-80'inde başlatın.
- Bileşen bellekten kaldırıldığında (unmount) animasyonları sonlandırın (bellek sızıntısını önleyin).

---

## 3. SVG Animasyonları

### SVG Animasyon Türleri

| Tür | Teknik | Kullanım Durumu |
|------|-----------|----------|
| **Çizgi Çizimi** | stroke-dashoffset | Logo açılışları, imzalar |
| **Morph (Dönüşüm)** | Path interpolasyonu | İkon geçişleri |
| **Transform** | rotate, scale, translate | Etkileşimli ikonlar |
| **Renk** | fill/stroke geçişi | Durum değişiklikleri |

### Çizgi Çizimi Prensipleri

```
stroke-dashoffset çizimi nasıl çalışır:
├── dasharray değerini yol (path) uzunluğuna eşitleyin
├── dashoffset değerini dasharray'e eşitleyin (gizli durum)
├── dashoffset değerini 0'a anime edin (açığa çıkan durum)
└── "Çizilme" efekti yaratın
```

### SVG Animasyonları Ne Zaman Kullanılır?

- ✅ Logo açılışları, marka anları
- ✅ İkon durum geçişleri (hamburger menü ↔ X)
- ✅ İnfografikler, veri görselleştirme
- ✅ Etkileşimli illüstrasyonlar
- ❌ Foto-gerçekçi içerikler (video kullanın)
- ❌ Çok karmaşık sahneler (performans sorunu yaratabilir)

### Prensipler

- Doğruluk için yol (path) uzunluğunu dinamik olarak alın.
- Süre: Tam çizimler için 1-3sn arası.
- Easing: Doğal bir his için ease-out.
- Basit dolgu renkleri (fills) animasyonu desteklemeli, onunla yarışmamalıdır.

---

## 4. 3B (3D) CSS Transformları

### Temel Özellikler

```
CSS 3B Alanı:
├── perspective: 3B alanın derinliği (genellikle 500-1500px)
├── transform-style: preserve-3d (çocuk öğeler için 3B'yi etkinleştirir)
├── rotateX/Y/Z: Eksen başına döndürme
├── translateZ: İzleyiciye yaklaşma/uzaklaşma
└── backface-visibility: Arka yüzün görünürlüğü
```

### Yaygın 3B Desenleri

| Desen | Kullanım Durumu |
|---------|----------|
| **Kart çevirme** | Gizli bilgiler, ürün görünümleri |
| **Hover'da eğilme (Tilt)** | Etkileşimli kartlar, 3B derinlik hissi |
| **Parallax katmanları** | Hero bölümleri, derinlikli kaydırma |
| **3B atlıkarınca (carousel)** | Görsel galerileri, sliderlar |

### Prensipler

- Perspektif: Hafif etki için 800-1200px, dramatik etki için 400-600px.
- Transformları basit tutun (döndürme + taşıma).
- Çevirme işlemlerinde `backface-visibility: hidden` durumundan emin olun.
- Safari tarayıcısında test edin (farklı işleme yapabilir).

---

## 5. Parçacık (Particle) Efektleri

### Parçacık Sistemi Türleri

| Tür | Hissi | Kullanım Durumu |
|------|------|----------|
| **Geometrik** | Teknoloji, ağ (network) | SaaS, teknoloji siteleri |
| **Konfeti** | Kutlama | Başarı anları |
| **Kar/Yağmur** | Atmosferik | Mevsimsel, ruh hali |
| **Toz/Bokeh** | Rüya gibi | Fotoğrafçılık, lüks |
| **Ateşböcekleri** | Büyülü | Oyunlar, fantezi |

### Kütüphaneler

| Kütüphane | En İyi Kullanım |
|---------|----------|
| **tsParticles** | Yapılandırılabilir, hafif |
| **particles.js** | Basit arka planlar |
| **Canvas API** | Özel tasarım, maksimum kontrol |
| **Three.js** | Karmaşık 3B parçacıklar |

### Prensipler

- Varsayılan: 30-50 parçacık (boğucu olmamalı).
- Hareket: Yavaş, organik (hız 0.5-2 arası).
- Opaklık: 0.3-0.6 (içerikle yarışmamalıdır).
- Bağlantılar: "Ağ" hissi için ince çizgiler.
- ⚠️ Mobilde devre dışı bırakın veya sayıyı azaltın.

### Ne Zaman Kullanılır?

- ✅ Hero arka planları (atmosferik etki)
- ✅ Başarı kutlamaları (konfeti patlaması)
- ✅ Teknoloji görselleştirme (bağlı düğümler)
- ❌ İçerik yoğunluğu fazla olan sayfalar (dikkat dağıtır)
- ❌ Düşük güçlü cihazlar (pil tüketimi)

---

## 6. Kaydırma Tetiklemeli (Scroll-Driven) Animasyonlar

### Native CSS (Modern Yaklaşım)

```
CSS Kaydırma Zaman Çizelgeleri (Scroll Timelines):
├── animation-timeline: scroll() - döküman kaydırma
├── animation-timeline: view() - öğe görüş alanında
├── animation-range: giriş/çıkış eşikleri
└── JavaScript gerektirmez
```

### Prensipler

| Tetikleme Noktası | Kullanım |
|---------------|----------|
| **Entry 0%** | Öğe görüş alanına girmeye başladığında |
| **Entry 50%** | Yarısı görünür olduğunda |
| **Cover 50%** | Görüş alanında merkezlendiğinde |
| **Exit 100%** | Tamamen çıkış yaptığında |

### En İyi Pratikler

- Ortaya çıkma animasyonları: Girişin yaklaşık %25'inde başlatın.
- Parallax: Sürekli kaydırma ilerlemesini kullanın.
- Sabit (sticky) öğeler: `cover` aralığını kullanın.
- Kaydırma performansını her zaman test edin.

---

## 7. Performans Prensipleri

### GPU ve CPU Animasyonu Farkı

```
UCUZ / KOLAY (GPU hızlandırmalı):
├── transform (translate, scale, rotate)
├── opacity
└── filter (idareli kullanın)

PAHALI / ZOR (Yeniden düzenleme tetikler):
├── width, height
├── top, left, right, bottom
├── padding, margin
└── karmaşık box-shadow (gölge)
```

### Optimizasyon Kontrol Listesi

- [ ] Sadece transform/opacity değerlerini anime edin.
- [ ] Ağır animasyonlardan önce `will-change` kullanın (sonra kaldırın).
- [ ] Düşük donanımlı cihazlarda test edin.
- [ ] `prefers-reduced-motion` tercihini uygulayın.
- [ ] Animasyon kütüphanelerini tembel yükle (lazy load) ile getirin.
- [ ] Kaydırma tabanlı hesaplamaları kısıtlayın (throttle).

---

## 8. Hareketli Grafik Karar Ağacı

```
Hangi animasyona ihtiyacınız var?
│
├── Karmaşık markalı animasyon?
│   └── Lottie (After Effects çıktısı)
│
├── Sıralı ve kaydırma tetiklemeli mi?
│   └── GSAP + ScrollTrigger
│
├── Logo veya ikon animasyonu mu?
│   └── SVG animasyonu (çizgi veya morph)
│
├── Etkileşimli 3B efekti mi?
│   └── CSS 3B Transformları (basit) veya Three.js (karmaşık)
│
├── Atmosferik arka plan mı?
│   └── tsParticles veya Canvas
│
└── Basit giriş veya hover mı?
    └── CSS @keyframes veya Framer Motion
```

---

## 9. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Her şeyi aynı anda anime etmek | Kademeli ve sıralı ilerleyin |
| Basit etkiler için ağır kütüphaneler kullanmak | CSS ile başlayın |
| Hareketi azaltma tercihini görmezden gelmek | Her zaman yedek (fallback) sunun |
| Ana iş parçacığını (thread) tıkamak | 60fps için optimize edin |
| Her projede aynı parçacıkları kullanmak | Markaya/bağlama uygun olanı seçin |
| Mobilde karmaşık etkiler kullanmak | Özellik algılama (feature detection) yapın |

---

## 10. Hızlı Referans

| Efekt | Araç | Performans |
|--------|------|-------------|
| Yükleme spinnerı | CSS/Lottie | Hafif |
| Kademeli ortaya çıkma | GSAP/Framer | Orta |
| SVG yol çizimi | CSS stroke | Hafif |
| 3B kart çevirme | CSS transform | Hafif |
| Parçacıklı arka plan | tsParticles | Ağır |
| Kaydırma parallaxı | GSAP ScrollTrigger | Orta |
| Şekil değiştirme (Morph) | GSAP MorphSVG | Orta |

---

> **Unutmayın**: Hareketli grafikler deneyimi geliştirmeli, dikkati dağıtmamalıdır. Her animasyon bir AMACA hizmet etmelidir: geri bildirim, rehberlik, keyif veya hikaye anlatımı.
