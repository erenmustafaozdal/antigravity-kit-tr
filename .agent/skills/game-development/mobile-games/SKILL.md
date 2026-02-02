---
name: mobile-games
description: Mobil oyun geliştirme prensipleri. Dokunma girdisi, pil ömrü, performans, uygulama mağazaları.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# Mobil Oyun Geliştirme (Mobile Game Development)

> Platform kısıtlamaları ve optimizasyon prensipleri.

---

## 1. Platform Hususları

### Temel Kısıtlamalar

| Kısıtlama | Strateji |
|------------|----------|
| **Dokunma Girdisi** | Geniş tıklama alanları, jestler |
| **Pil Ömrü** | CPU/GPU kullanımını sınırla |
| **Isınma (Thermal)** | Isındığında performansı düşür (throttle) |
| **Ekran Boyutu** | Duyarlı (responsive) arayüz |
| **Kesintiler** | Arka plana atıldığında oyunu duraklat |

---

## 2. Dokunma Girdisi Prensipleri

### Dokunma (Touch) vs Kumanda (Controller)

| Dokunma | Masaüstü/Konsol |
|-------|-----------------|
| Hassas değil | Hassas |
| Ekranı kapatır | Görüşü engellemez |
| Sınırlı buton sayısı | Çok sayıda buton |
| Jestler mevcut | Butonlar/analog çubuklar |

### En İyi Pratikler

- Minimum dokunma hedefi: 44x44 puan (points).
- Dokunma anında görsel geri bildirim.
- Çok hassas zamanlama gereksinimlerinden kaçının.
- Hem dikey (portrait) hem de yatay (landscape) modu destekleyin.

---

## 3. Performans Hedefleri

### Isı Yönetimi (Thermal Management)

| Eylem | Tetikleyici |
|--------|---------|
| Kaliteyi düşür | Cihaz ısındığında |
| FPS'i sınırla | Cihaz çok ısındığında |
| Efektleri durdur | Kritik sıcaklık seviyesinde |

### Pil Optimizasyonu

- 30 FPS genellikle yeterlidir.
- Duraklatıldığında uyku moduna geçin.
- GPS/Ağ kullanımını minimuma indirin.
- Karanlık mod (dark mode) OLED pillerde tasarruf sağlar.

---

## 4. Uygulama Mağazası Gereksinimleri

### iOS (App Store)

| Gereksinim | Not |
|-------------|------|
| Gizlilik etiketleri | Zorunlu |
| Hesap silme | Hesap oluşturma varsa zorunlu |
| Ekran görüntüleri | Tüm cihaz boyutları için |

### Android (Google Play)

| Gereksinim | Not |
|-------------|------|
| Hedef API | Mevcut yılın SDK'sı |
| 64-bit desteği | Zorunlu |
| App bundles | Tavsiye edilir |

---

## 5. Gelir Modelleri (Monetization)

| Model | En Uygun Kullanım |
|-------|----------|
| **Premium** | Kaliteli oyunlar, sadık kitle |
| **Ücretsiz + IAP** | Gündelik, ilerleme odaklı oyunlar |
| **Reklamlar** | Hiper-gündelik, yüksek hacimli oyunlar |
| **Abonelik** | İçerik güncellemeleri, çok oyunculu |

---

## 6. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Masaüstü kontrollerini aynen aktarmak | Dokunmatik için tasarlayın |
| Pil tüketimini görmezden gelmek | Isı değerlerini izleyin |
| Yatay modu zorunlu tutmak | Oyuncu tercihine saygı duyun |
| Her zaman açık internet zorunluluğu | Önbelleğe alın ve senkronize edin |

---

> **Unutmayın:** Mobil, en kısıtlı platformdur. Pile ve oyuncunun dikkat süresine saygı duyun.
