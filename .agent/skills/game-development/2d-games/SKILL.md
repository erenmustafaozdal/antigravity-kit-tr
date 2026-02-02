---
name: 2d-games
description: 2B oyun geliştirme prensipleri. Sprite'lar, tilemap'ler, fizik, kamera.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# 2B Oyun Geliştirme (2D Game Development)

> 2B oyun sistemleri için temel prensipler.

---

## 1. Sprite Sistemleri

### Sprite Organizasyonu

| Bileşen | Amaç |
|-----------|---------|
| **Atlas** | Dokuları birleştirir, çizim çağrılarını (draw calls) azaltır |
| **Animasyon** | Kare (frame) dizileri |
| **Pivot** | Döndürme/ölçeklendirme başlangıç noktası |
| **Katmanlama (Layering)** | Z-sırası (Z-order) kontrolü |

### Animasyon Prensipleri

- Kare hızı: Genellikle 8-24 FPS arası.
- Etki için "ezme ve esnetme" (squash and stretch).
- Eylemden önce "beklenti" (anticipation).
- Eylemden sonra "takip" (follow-through).

---

## 2. Tilemap Tasarımı

### Karo (Tile) Hususları

| Faktör | Öneri |
|--------|----------------|
| **Boyut** | 16x16, 32x32, 64x64 |
| **Otomatik Karolama (Auto-tiling)** | Arazi (terrain) için kullanın |
| **Çarpışma (Collision)** | Basitleştirilmiş şekiller kullanın |

### Katmanlar (Layers)

| Katman | İçerik |
|-------|---------|
| Arkaplan (Background) | Etkileşimsiz manzara |
| Arazi (Terrain) | Üzerinde yürünebilir zemin |
| Dekorlar (Props) | Etkileşimli nesneler |
| Önplan (Foreground) | Parallax katmanı |

---

## 3. 2B Fizik

### Çarpışma Şekilleri (Collision Shapes)

| Şekil | Kullanım Durumu |
|-------|----------|
| Box (Kutu) | Dikdörtgen nesneler |
| Circle (Daire) | Toplar, yuvarlak nesneler |
| Capsule (Kapsül) | Karakterler |
| Polygon (Çokgen) | Karmaşık şekiller |

### Fizik Hususları

- Piksel-mükemmel (pixel-perfect) vs fizik-tabanlı yaklaşım seçimi.
- Tutarlılık için sabit zaman adımı (fixed timestep).
- Filtreleme için katmanlar (layers).

---

## 4. Kamera Sistemleri

### Kamera Türleri

| Tür | Kullanım |
|------|-----|
| **Takip (Follow)** | Oyuncuyu takip eder |
| **İleri Bakış (Look-ahead)** | Hareketi daha önceden görür |
| **Çoklu Hedef (Multi-target)** | İki kişilik oyunlar için |
| **Oda Temelli (Room-based)** | Metroidvania türü oyunlar |

### Ekran Sallantısı (Screen Shake)

- Kısa süre (50-200ms).
- Azalan yoğunlukta olmalı.
- İdareli kullanın.

---

## 5. Tür Desenleri (Genre Patterns)

### Platformer

- Coyote time (kenardan düştükten sonraki tolerans süresi).
- Jump buffering (zeminle temas etmeden az önce zıplama komutu verme).
- Değişken zıplama yüksekliği (tuşa basılı tutma süresine göre).

### Üstten Görünüm (Top-down)

- 8 yönlü veya serbest hareket.
- Nişan alma tabanlı veya otomatik nişan alma.
- Döndürme (rotation) kullanımı veya sabit yön.

---

## 6. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Ayrı dokular kullanmak | Atlaslar (atlases) kullanın |
| Karmaşık çarpışma şekilleri | Basitleştirilmiş çarpışma şekilleri |
| Sarsıntılı kamera | Yumuşak takip (smoothing) |
| Fizik üzerinde piksel-mükemmellik zorlamak | Tek bir yaklaşım seçin |

---

> **Unutmayın:** 2B açıklık ve netlik üzerinedir. Her piksel bir şey anlatmalıdır.
