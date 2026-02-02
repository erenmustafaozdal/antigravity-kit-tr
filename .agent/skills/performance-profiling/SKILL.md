---
name: performance-profiling
description: Performans profilleme prensipleri. Ölçüm, analiz ve optimizasyon teknikleri.
allowed-tools: Read, Glob, Grep, Bash
---

# Performans Profilleme (Performance Profiling)

> Ölç, analiz et, optimize et - bu sırayla.

## 🔧 Çalışma Zamanı Script'leri

**Otomatik profilleme için bunları çalıştırın:**

| Script | Amaç | Kullanım |
|--------|------|----------|
| `scripts/lighthouse_audit.py` | Lighthouse performans denetimi | `python scripts/lighthouse_audit.py https://example.com` |

---

## 1. Core Web Vitals

### Hedefler

| Metrik | İyi | Kötü | Ölçer |
|--------|-----|------|-------|
| **LCP** | < 2.5s | > 4.0s | Yükleme |
| **INP** | < 200ms | > 500ms | Etkileşim |
| **CLS** | < 0.1 | > 0.25 | Stabilite |

### Ne Zaman Ölçülür

| Aşama | Araç |
|-------|------|
| Geliştirme | Yerel Lighthouse |
| CI/CD | Lighthouse CI |
| Prodüksiyon | RUM (Real User Monitoring) |

---

## 2. Profilleme İş Akışı

### 4 Adımlı Süreç

```
1. BASELINE → Mevcut durumu ölç
2. IDENTIFY → Darboğazı bul
3. FIX → Hedefli değişiklik yap
4. VALIDATE → İyileştirmeyi doğrula
```

### Profilleme Aracı Seçimi

| Sorun | Araç |
|-------|------|
| Sayfa yüklemesi | Lighthouse |
| Paket boyutu | Bundle analyzer |
| Çalışma zamanı | DevTools Performance |
| Bellek | DevTools Memory |
| Ağ | DevTools Network |

---

## 3. Paket Analizi

### Neye Bakılır

| Sorun | Gösterge |
|-------|----------|
| Büyük bağımlılıklar | Paketin en üstünde |
| Yinelenen kod | Birden fazla chunk |
| Kullanılmayan kod | Düşük kapsam |
| Eksik bölünmeler | Tek büyük chunk |

### Optimizasyon Eylemleri

| Bulgu | Eylem |
|-------|-------|
| Büyük kütüphane | Belirli modülleri içe aktar |
| Yinelenen bağımlılıklar | Dedup, versiyonları güncelle |
| Ana rota | Kod bölme |
| Kullanılmayan export'lar | Tree shake |

---

## 4. Çalışma Zamanı Profilleme

### Performance Sekmesi Analizi

| Desen | Anlam |
|-------|-------|
| Uzun görevler (>50ms) | UI bloke |
| Birçok küçük görev | Toplu işleme fırsatı |
| Layout/paint | Rendering darboğazı |
| Script | JavaScript yürütme |

### Memory Sekmesi Analizi

| Desen | Anlam |
|-------|-------|
| Büyüyen heap | Olası sızıntı |
| Büyük tutulma | Referansları kontrol et |
| Ayrılmış DOM | Temizlenmedi |

---

## 5. Yaygın Darboğazlar

### Belirtiye Göre

| Belirti | Olası Neden |
|---------|-------------|
| Yavaş ilk yükleme | Büyük JS, render bloke |
| Yavaş etkileşimler | Ağır event handler'lar |
| Scroll sırasında jank | Layout thrashing |
| Büyüyen bellek | Sızıntılar, tutulmuş ref'ler |

---

## 6. Hızlı Kazanım Öncelikleri

| Öncelik | Eylem | Etki |
|---------|-------|------|
| 1 | Sıkıştırmayı etkinleştir | Yüksek |
| 2 | Görselleri lazy load yap | Yüksek |
| 3 | Rotaları kod bölme | Yüksek |
| 4 | Statik varlıkları önbelleğe al | Orta |
| 5 | Görselleri optimize et | Orta |

---

## 7. Anti-Desenler

| ❌ Yapma | ✅ Yap |
|----------|--------|
| Sorunları tahmin et | Önce profillle |
| Mikro-optimize et | En büyük sorunu düzelt |
| Erken optimize et | Gerektiğinde optimize et |
| Gerçek kullanıcıları görmezden gel | RUM verilerini kullan |

---

> **Unutma:** En hızlı kod, çalışmayan koddur. Optimize etmeden önce kaldır.
