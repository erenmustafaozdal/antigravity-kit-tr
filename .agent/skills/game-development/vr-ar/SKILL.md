---
name: vr-ar
description: VR/AR geliştirme prensipleri. Konfor, etkileşim, performans gereksinimleri.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# VR/AR Geliştirme (VR/AR Development)

> Derinlikli (Immersive) deneyim prensipleri.

---

## 1. Platform Seçimi

### VR Platformları

| Platform | Kullanım Durumu |
|----------|----------|
| **Quest** | Bağımsız (Standalone), kablosuz |
| **PCVR** | Yüksek sadakat (High fidelity) |
| **PSVR** | Konsol pazarı |
| **WebXR** | Tarayıcı tabanlı |

### AR Platformları

| Platform | Kullanım Durumu |
|----------|----------|
| **ARKit** | iOS cihazlar |
| **ARCore** | Android cihazlar |
| **WebXR** | Tarayıcı AR |
| **HoloLens** | Kurumsal çözümler |

---

## 2. Konfor Prensipleri

### Hareket Hastalığını (Motion Sickness) Önleme

| Neden | Çözüm |
|-------|----------|
| **Yer Değiştirme (Locomotion)** | Teleport (ışınlanma), ani dönüş |
| **Düşük FPS** | Sabit 90 FPS koru |
| **Kamera Sarsıntısı** | Kaçın veya minimuma indir |
| **Hızlı İvmelenme** | Kademeli hareket |

### Konfor Ayarları

- Hareket sırasında kenar karartma (Vignette).
- Ani (Snap) vs yumuşak (Smooth) dönüş seçenekleri.
- Oturarak vs ayakta oynama modları.
- Boy kalibrasyonu.

---

## 3. Performans Gereksinimleri

### Hedef Metrikler

| Platform | FPS | Çözünürlük |
|----------|-----|------------|
| Quest 2 | 72-90 | 1832x1920 |
| Quest 3 | 90-120 | 2064x2208 |
| PCVR | 90 | 2160x2160+ |
| PSVR2 | 90-120 | 2000x2040 |

### Kare Bütçesi

- VR, tutarlı kare süreleri (consistent frame times) gerektirir.
- Tek bir düşen kare = görünür sarsıntı (judder).
- 90 FPS = 11.11ms işlem bütçesi.

---

## 4. Etkileşim Prensipleri

### Kontrolcü Etkileşimi

| Tür | Kullanım |
|------|-----|
| **İşaretle + Tıkla** | Arayüz (UI), uzak nesneler |
| **Tutma (Grab)** | Nesne manipülasyonu |
| **Jest (Gesture)** | Büyü, özel eylemler |
| **Fiziksel** | Fırlatma, savurma |

### El Takibi (Hand Tracking)

- Daha derin hissettirir ama daha az hassastır.
- Uygun olduğu alanlar: Sosyal etkileşim, gündelik oyunlar.
- Zorlayıcı olduğu alanlar: Aksiyon, yüksek hassasiyet gerektiren işler.

---

## 5. Mekansal Tasarım (Spatial Design)

### Dünya Ölçeği

- 1 birim = 1 metre (kritiktir).
- Nesneler doğru boyutta hissettirmelidir.
- Gerçek dünya ölçüleriyle test edin.

### Derinlik İpuçları (Depth Cues)

| İpucu | Önem Derecesi |
|-----|------------|
| Stereo (Çift Göz) | Birincil derinlik |
| Hareket Parallaxı | İkincil |
| Gölgeler | Konum sabitleme (Grounding) |
| Örtme (Occlusion) | Katmanlama |

---

## 6. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Kamerayı oyuncudan bağımsız hareket ettirmek | Kamera kontrolü oyuncuda olmalı |
| 90 FPS'in altına düşmek | Kare hızını sabit tutun |
| Çok küçük arayüz metinleri kullanmak | Büyük ve okunabilir metinler kullanın |
| Kol mesafesini görmezden gelmek | Oyuncunun erişim alanına göre ölçekleyin |

---

> **Unutmayın:** Konfor isteğe bağlı değildir. Midesi bulanan oyuncu oynamaz.
