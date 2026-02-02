---
name: game-development
description: Oyun geliştirme orkestratörü. Proje ihtiyaçlarına göre platforma özel yeteneklere yönlendirir.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Oyun Geliştirme (Game Development)

> Temel prensipleri sağlayan ve uzmanlaşmış alt yeteneklere yönlendiren **orkestratör yetenek**.

---

## Bu Yetenek Ne Zaman Kullanılır?

Bir oyun geliştirme projesi üzerinde çalışıyorsunuz. Bu yetenek size oyun geliştirmenin PRENSİPLERİNİ öğretir ve bağlama göre sizi doğru alt yeteneğe yönlendirir.

---

## Alt Yetenek Yönlendirmesi

### Platform Seçimi

| Hedef platform... | Kullanılacak Alt Yetenek |
|------------------------|---------------|
| Web tarayıcıları (HTML5, WebGL) | `game-development/web-games` |
| Mobil (iOS, Android) | `game-development/mobile-games` |
| PC (Steam, Masaüstü) | `game-development/pc-games` |
| VR/AR cihazları | `game-development/vr-ar` |

### Boyut Seçimi

| Oyun türü... | Kullanılacak Alt Yetenek |
|-------------------|---------------|
| 2B (sprite'lar, tilemap'ler) | `game-development/2d-games` |
| 3B (mesh'ler, shader'lar) | `game-development/3d-games` |

### Uzmanlık Alanları

| Şunlara ihtiyacınız varsa... | Kullanılacak Alt Yetenek |
|----------------|---------------|
| GDD, dengeleme, oyuncu psikolojisi | `game-development/game-design` |
| Çok oyunculu (Multiplayer), ağ iletişimi | `game-development/multiplayer` |
| Görsel stil, varlık (asset) boru hattı, animasyon | `game-development/game-art` |
| Ses tasarımı, müzik, adaptif ses | `game-development/game-audio` |

---

## Temel Prensipler (Tüm Platformlar)

### 1. Oyun Döngüsü (The Game Loop)

Platformdan bağımsız olarak her oyun şu deseni takip eder:

```
INPUT (GİRDİ)  → Oyuncu eylemlerini oku
UPDATE (GÜNCELLE) → Oyun mantığını işle (fixed timestep)
RENDER (ÇİZ) → Kareyi ekrana çiz (interpolated)
```

**Sabit Zaman Adımı (Fixed Timestep) Kuralı:**
- Fizik/Mantık: Sabit hızda (örneğin 50Hz)
- Çizim: Mümkün olduğunca hızlı
- Akıcı görseller için durumlar arasında interpolasyon (ara değer bulma) yapın.

---

### 2. Desen Seçim Matrisi

| Desen | Ne Zaman Kullanılır | Örnek |
|---------|----------|---------|
| **Durum Makinesi (State Machine)** | 3-5 belirgin durum varsa | Oyuncu: Bekleme→Yürüme→Zıplama |
| **Nesne Havuzu (Object Pooling)** | Sık yaratma/yok etme varsa | Mermiler, parçacıklar |
| **Gözlemci/Olaylar (Observer/Events)** | Sistemler arası iletişim | Sağlık Durumu→UI güncellemeleri |
| **ECS (Entity Component System)** | Binlerce benzer varlık varsa | RTS birimleri, parçacıklar |
| **Komut (Command)** | Geri alma, replay, ağ iletişimi | Girdi kaydetme |
| **Davranış Ağacı (Behavior Tree)** | Karmaşık YZ kararları | Düşman YZ |

**Karar Kuralı:** Durum Makinesi ile başlayın. ECS'yi sadece performans gerektirdiğinde ekleyin.

---

### 3. Girdi Soyutlama (Input Abstraction)

Girdiyi ham tuşlar yerine EYLEMLERE (ACTIONS) soyutlayın:

```
"zipla"  → Boşluk, Oyun kumandası A, Dokunma
"hareket"  → WASD, Sol çubuk, Sanal joystick
```

**Neden:** Çoklu platform desteği ve yeniden atanabilir kontroller sağlar.

---

### 4. Performans Bütçesi (60 FPS = 16.67ms)

| Sistem | Bütçe |
|--------|--------|
| Girdi | 1ms |
| Fizik | 3ms |
| YZ (AI) | 2ms |
| Oyun Mantığı | 4ms |
| Çizim (Rendering) | 5ms |
| Tampon (Buffer) | 1.67ms |

**Optimizasyon Önceliği:**
1. Algoritma (O(n²) → O(n log n))
2. Gruplama (Batching - çizim çağrılarını azaltma)
3. Havuzlama (Pooling - bellek temizleme sıçramalarını önleme)
4. LOD (Uzaklığa göre detay seviyesi ayarlama)
5. Ayıklama (Culling - görünmeyenleri pas geçme)

---

### 5. Karmaşıklığa Göre YZ Seçimi

| YZ Türü | Karmaşıklık | Ne Zaman Kullanılır |
|---------|------------|----------|
| **FSM (Durum Makinesi)**| Basit | 3-5 durum, tahmin edilebilir davranış |
| **Davranış Ağacı** | Orta | Modüler, tasarımcı dostu |
| **GOAP** | Yüksek | Ortaya çıkan (emergent), planlama tabanlı |
| **Utility AI** | Yüksek | Puanlama tabanlı kararlar |

---

### 6. Çarpışma (Collision) Stratejisi

| Tür | En Uygun Kullanım |
|------|----------|
| **AABB** | Dikdörtgenler, hızlı kontroller |
| **Daire (Circle)** | Yuvarlak nesneler, maliyet düşük |
| **Spatial Hash** | Çok sayıda benzer boyutlu nesne |
| **Quadtree** | Büyük dünyalar, değişken boyutlar |

---

## Anti-Desenler (Evrensel)

| YAPMAYIN | YAPIN |
|-------|-----|
| Her karede her şeyi güncelleyin | Olayları (events), kirli bayrakları (dirty flags) kullanın |
| Sıcak döngülerde nesne yaratın | Nesne havuzlama (object pooling) kullanın |
| Hiçbir şeyi önbelleğe almayın | Referansları önbelleğe alın |
| Profil oluşturmadan optimize edin | Önce profil (profiling) oluşturun |
| Girdiyi mantıkla karıştırın | Girdi katmanını soyutlayın |

---

## Yönlendirme Örnekleri

### Örnek 1: "Tarayıcı tabanlı 2B platform oyunu yapmak istiyorum"
→ Framework seçimi için `game-development/web-games` ile başlayın.
→ Ardından sprite/tilemap desenleri için `game-development/2d-games` yeteneğini kullanın.
→ Bölüm tasarımı için `game-development/game-design` referansına bakın.

### Örnek 2: "iOS ve Android için mobil bulmaca oyunu"
→ Dokunma girdisi ve mağazalar için `game-development/mobile-games` ile başlayın.
→ Bulmaca dengeleme için `game-development/game-design` kullanın.

### Örnek 3: "Çok oyunculu VR shooter (nişancı)"
→ Konfor ve daldırma (immersion) için `game-development/vr-ar`.
→ Çizim için `game-development/3d-games`.
→ Ağ iletişimi için `game-development/multiplayer`.

---

> **Unutmayın:** Harika oyunlar mükemmellikten değil, yinelemeden (iteration) doğar. Hızlıca prototip üretin, sonra cilalayın.
