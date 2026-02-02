---
name: 3d-games
description: 3B oyun geliştirme prensipleri. Çizim, shader'lar, fizik, kameralar.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# 3B Oyun Geliştirme (3D Game Development)

> 3B oyun sistemleri için temel prensipler.

---

## 1. Çizim Hattı (Rendering Pipeline)

### Aşamalar

```
1. Vertex Processing (Köşe İşleme) → Geometriyi dönüştür
2. Rasterization (Rasterizasyon) → Piksellere dönüştür
3. Fragment Processing (Fragman İşleme) → Pikselleri renklendir
4. Output (Çıktı) → Ekrana gönder
```

### Optimizasyon Prensipleri

| Teknik | Amaç |
|-----------|---------|
| **Frustum culling** | Ekran dışındakileri çizme |
| **Occlusion culling**| Gizli/kapatılmış olanları çizme |
| **LOD (Detay Seviyesi)**| Uzaklıktaki detayı azalt |
| **Batching (Gruplama)**| Çizim çağrılarını birleştir |

---

## 2. Shader Prensipleri

### Shader Türleri

| Tür | Amaç |
|------|---------|
| **Vertex** | Konum, normaller |
| **Fragment/Pixel**| Renk, ışıklandırma |
| **Compute** | Genel hesaplama işlemleri |

### Ne Zaman Özel Shader Yazılmalı?

- Özel efektler (su, ateş, portallar).
- Stilize çizimler (toon shading, karakalem efekti).
- Performans optimizasyonu.
- Benzersiz bir görsel kimlik yaratma.

---

## 3. 3B Fizik

### Çarpışma Şekilleri (Collision Shapes)

| Şekil | Kullanım Durumu |
|-------|----------|
| **Box (Kutu)** | Binalar, kasalar |
| **Sphere (Küre)** | Toplar, hızlı kontroller |
| **Capsule (Kapsül)**| Karakterler |
| **Mesh** | Arazi (Terrain - maliyetlidir) |

### Prensipler

- Basit çarpıştırıcılar (colliders), karmaşık görseller.
- Katman tabanlı filtreleme.
- Görüş hattı (line-of-sight) için Raycasting.

---

## 4. Kamera Sistemleri

### Kamera Türleri

| Tür | Kullanım |
|------|-----|
| **Üçüncü Şahıs (Third-person)**| Aksiyon, macera |
| **Birinci Şahıs (First-person)**| Daldırma (Immersive), FPS |
| **İzometrik** | Strateji, RPG |
| **Orbital** | İnceleme, editörler |

### Kamera Hissi

- Yumuşak takip (lerp/smoothing).
- Çarpışma engelleme (duvarların içine girmeme).
- Hareket için ileri bakış (look-ahead).
- Hız hissi için FOV (görüş alanı) değişiklikleri.

---

## 5. Işıklandırma (Lighting)

### Işık Türleri

| Tür | Kullanım |
|------|-----|
| **Directional (Yönlü)**| Güneş, ay |
| **Point (Noktasal)** | Lambalar, meşaleler |
| **Spot** | El feneri, sahne ışığı |
| **Ambient (Ortam)** | Temel aydınlatma |

### Performans Hususları

- Gerçek zamanlı (real-time) gölgeler maliyetlidir.
- Mümkünse "Bake" (önceden hesaplanmış) yapın.
- Büyük dünyalar için gölge kaskadları (shadow cascades) kullanın.

---

## 6. Detay Seviyesi (Level of Detail - LOD)

### LOD Stratejisi

| Uzaklık | Model |
|----------|-------|
| Yakın | Tam detay |
| Orta | %50 poligon sayısı |
| Uzak | %25 veya billboard (2B düzlem) |

---

## 7. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Her yerde Mesh Collider kullanmak | Basit şekiller kullanın |
| Mobilde gerçek zamanlı gölgeler kullanmak | Bake edilmiş veya blob gölgeler kullanın |
| Tüm mesafeler için tek bir LOD kullanmak | Mesafe tabanlı LOD kullanın |
| Optimize edilmemiş shader'lar | Profil oluşturun ve basitleştirin |

---

> **Unutmayın:** 3B bir illüzyondur. Detayın kendisini değil, detayın izlenimini yaratın.
