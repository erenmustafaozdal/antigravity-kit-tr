---
name: pc-games
description: PC ve konsol oyun geliştirme prensipleri. Motor seçimi, platform özellikleri, optimizasyon stratejileri.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# PC/Konsol Oyun Geliştirme (PC/Console Game Development)

> Motor seçimi ve platforma özel prensipler.

---

## 1. Motor (Engine) Seçimi

### Karar Ağacı

```
Ne inşa ediyorsunuz?
│
├── 2B Oyun
│   ├── Açık kaynak önemli mi? → Godot
│   └── Büyük ekip/varlık (asset) yönetimi mi? → Unity
│
├── 3B Oyun
│   ├── AAA görsel kalite mi? → Unreal
│   ├── Çoklu platform önceliği mi? → Unity
│   └── Bağımsız / Açık kaynak mı? → Godot 4
│
└── Özel İhtiyaçlar
    ├── DOTS performans mı? → Unity
    ├── Nanite/Lumen mi? → Unreal
    └── Hafif ve hızlı mı? → Godot
```

### Karşılaştırma

| Faktör | Unity 6 | Godot 4 | Unreal 5 |
|--------|---------|---------|----------|
| 2B (2D) | İyi | Mükemmel | Sınırlı |
| 3B (3D) | İyi | İyi | Mükemmel |
| Öğrenme | Orta | Kolay | Zor |
| Maliyet | Gelir payı | Ücretsiz | 1M$ sonrası %5 |
| Ekip Yapısı | Her boyutta | Tekil-Orta | Orta-Büyük |

---

## 2. Platform Özellikleri

### Steam Entegrasyonu

| Özellik | Amaç |
|---------|---------|
| Başarımlar (Achievements)| Oyuncu hedefleri |
| Bulut Kayıtları | Cihazlar arası ilerleme |
| Liderlik Tabloları | Rekabet |
| Workshop (Atölye) | Kullanıcı modları |
| Zengin Varlık (Rich Presence)| Oyun içi durumu gösterme |

### Konsol Gereksinimleri

| Platform | Sertifikasyon |
|----------|--------------|
| PlayStation | TRC uyumluluğu |
| Xbox | XR uyumluluğu |
| Nintendo | Lotcheck |

---

## 3. Kontrolcü (Controller) Desteği

### Girdi Soyutlama

```
Butonları değil, EYLEMLERİ (ACTIONS) eşleştirin:
- "onayla" → A (Xbox), Cross (PS), B (Nintendo)
- "iptal" → B (Xbox), Circle (PS), A (Nintendo)
```

### Dokunsal Geri Bildirim (Haptic Feedback)

| Yoğunluk | Kullanım |
|-----------|-----|
| Hafif | UI geri bildirimi |
| Orta | Çarpışmalar, darbeler |
| Güçlü | Büyük olaylar |

---

## 4. Performans Optimizasyonu

### Önce Profil Oluşturma (Profiling)

| Motor | Araç |
|--------|------|
| Unity | Profiler Window |
| Godot | Debugger → Profiler |
| Unreal | Unreal Insights |

### Yaygın Darboğazlar

| Darboğaz | Çözüm |
|------------|----------|
| Çizim çağrıları (Draw calls)| Batching (gruplama), atlaslar |
| GC sıçramaları | Nesne havuzlama (object pooling) |
| Fizik | Daha basit çarpıştırıcılar |
| Shader'lar | LOD shader'lar |

---

## 5. Motora Özel Prensipler

### Unity 6

- Performansın kritik olduğu yerlerde DOTS kullanımı.
- Sıcak yollar (hot paths) için Burst derleyicisi.
- Varlık akışı (asset streaming) için Addressables.

### Godot 4

- Hızlı yineleme için GDScript.
- Karmaşık mantık için C#.
- Bağlantıyı kesmek (decoupling) için Sinyaller (Signals).

### Unreal 5

- Tasarımcılar için Blueprint.
- Performans için C++.
- Yüksek poligonlu ortamlar için Nanite.
- Dinamik ışıklandırma için Lumen.

---

## 6. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Popülerliğe (hype) göre motor seçmek | Proje ihtiyaçlarına göre seçin |
| Platform yönergelerini yok saymak | Sertifikasyon gereksinimlerini inceleyin |
| Girdi butonlarını hardcode etmek | Eylemlere (actions) soyutlayın |
| Profil oluşturmayı atlamak | Erken ve sık sık profil oluşturun |

---

> **Unutmayın:** Oyun motoru sadece bir araçtır. Prensiplerde ustalaşın, sonra herhangi bir motora uyum sağlayın.
