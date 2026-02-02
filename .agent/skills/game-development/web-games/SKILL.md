---
name: web-games
description: Web tarayıcı oyun geliştirme prensipleri. Framework seçimi, WebGPU, optimizasyon, PWA.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# Web Tarayıcı Oyun Geliştirme (Web Browser Game Development)

> Framework seçimi ve tarayıcıya özel prensipler.

---

## 1. Framework Seçimi

### Karar Ağacı

```
Ne tür bir oyun?
│
├── 2B Oyun
│   ├── Tam oyun motoru özellikleri mi? → Phaser
│   └── Sadece ham çizim gücü mü? → PixiJS
│
├── 3B Oyun
│   ├── Tam motor (fizik, XR vb.) mi? → Babylon.js
│   └── Çizim odaklı mı? → Three.js
│
└── Hibrit / Canvas
    └── Özel çözüm → Saf Canvas/WebGL
```

### Karşılaştırma (2025)

| Framework | Tür | En Uygun |
|-----------|------|----------|
| **Phaser 4** | 2B | Eksiksiz oyun özellikleri |
| **PixiJS 8** | 2B | Çizim hızı, UI |
| **Three.js** | 3B | Görselleştirmeler, hafif yapı |
| **Babylon.js 7** | 3B | Tam teşekküllü motor, XR |

---

## 2. WebGPU Geçişi

### Tarayıcı Desteği (2025 başı)

| Tarayıcı | Destek Durumu |
|---------|---------|
| Chrome | ✅ v113'ten beri |
| Edge | ✅ v113'ten beri |
| Firefox | ✅ v131'den beri |
| Safari | ✅ 18.0'dan beri |
| **Toplam** | **~%73** küresel kullanım |

### Karar Stratejisi

- **Yeni projeler**: WebGL yedeği (fallback) ile WebGPU kullanın.
- **Eski cihaz desteği**: WebGL ile başlayın.
- **Özellik tespiti**: `navigator.gpu` kontrolü yapın.

---

## 3. Performans Prensipleri

### Tarayıcı Kısıtlamaları

| Kısıtlama | Strateji |
|------------|----------|
| Yerel dosya erişimi yok | Varlık paketleme, CDN kullanımı |
| Sekme sönümleme (throttling)| Gizlendiğinde oyunu duraklat |
| Mobil veri sınırları | Varlıkları sıkıştır |
| Ses otomatik oynatma engeli | Kullanıcı etkileşimi şartı |

### Optimizasyon Önceliği

1. **Varlık sıkıştırma** - KTX2, Draco, WebP.
2. **Tembel yükleme (Lazy loading)** - İhtiyaç anında yükle.
3. **Nesne havuzlama (Object pooling)** - Bellek temizliğinden (GC) kaçın.
4. **Çizim çağrısı gruplama** - Durum değişikliklerini azalt.
5. **Web Workers** - Ağır hesaplamaları ana iş parçacığından ayır.

---

## 4. Varlık (Asset) Stratejisi

### Sıkıştırma Formatları

| Tür | Format |
|------|--------|
| Dokular | KTX2 + Basis Universal |
| Ses | WebM/Opus (Yedek: MP3) |
| 3B Modeller | glTF + Draco/Meshopt |

### Yükleme Stratejisi

| Aşama | Ne Yüklenmeli? |
|-------|------|
| Başlangıç | Temel varlıklar, <2MB |
| Oynanış | İhtiyaç anında akış yap |
| Arka Plan | Bir sonraki bölümü önceden çek |

---

## 5. Oyunlar için PWA (Aşamalı Web Uygulaması)

### Avantajlar

- Çevrimdışı oynama.
- Ana ekrana yükleme.
- Tam ekran modu.
- Anlık bildirimler (push notifications).

### Gereksinimler

- Önbelleğe alma için Service Worker.
- Web App Manifest dosyası.
- HTTPS zorunluluğu.

---

## 6. Ses Yönetimi

### Tarayıcı Gereksinimleri

- Audio Context başlatmak için kullanıcı etkileşimi gerekir.
- İlk tıklama/dokunmada AudioContext oluşturun.
- Eğer askıya alınmışsa (suspended) bağlamı devam ettirin (resume).

### En İyi Pratikler

- Web Audio API kullanın.
- Ses kaynaklarını havuzlayın (pooling).
- Yaygın sesleri önceden yükleyin.
- WebM/Opus ile sıkıştırın.

---

## 7. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Tüm varlıkları en başta yüklemek | Kademeli yükleme (progressive) |
| Sekme görünürlüğünü yok saymak | Gizlendiğinde duraklatın |
| Ses yüklenene kadar akışı kesmek | Sesi tembel yükleyin |
| Sıkıştırmayı atlamak | Her şeyi sıkıştırın |
| Hızlı internet varsaymak | Yavaş ağları hesaba katın |

---

> **Unutmayın:** Tarayıcı en erişilebilir platformdur. Onun kısıtlamalarına saygı duyun.
