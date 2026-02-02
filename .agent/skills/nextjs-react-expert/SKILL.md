---
name: react-best-practices
description: Vercel Mühendisliğinden React ve Next.js performans optimizasyonu. React componentleri oluştururken, performansı optimize ederken, şelaleleri ortadan kaldırırken, paket boyutunu küçültürken, performans sorunları için kod incelerken veya sunucu/istemci tarafı optimizasyonları uygularken kullanın.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Next.js ve React Performans Uzmanı

> **Vercel Mühendisliğinden** - Etkiye göre önceliklendirilmiş 57 optimizasyon kuralı
> **Felsefe:** Önce şelaleleri ortadan kaldırın, sonra paketleri optimize edin, ardından mikro-optimizasyon yapın.

---

## 🎯 Seçici Okuma Kuralı (ZORUNLU)

**SADECE görevinizle ilgili bölümleri okuyun!** Aşağıdaki içerik haritasını kontrol edin ve ihtiyacınız olanı yükleyin.

> 🔴 **Performans incelemeleri için: Önce KRİTİK bölümlerle (1-2) başlayın, sonra YÜKSEK/ORTA'ya geçin.**

---

## 📑 İçerik Haritası

| Dosya | Etki | Kural Sayısı | Ne Zaman Okunmalı? |
|-------|------|--------------|---------------------|
| `1-async-eliminating-waterfalls.md` | 🔴 **KRİTİK** | 5 kural | Yavaş sayfa yüklemeleri, ardışık API çağrıları, veri çekme şelaleleri |
| `2-bundle-bundle-size-optimization.md` | 🔴 **KRİTİK** | 5 kural | Büyük paket boyutu, yavaş Time to Interactive, First Load sorunları |
| `3-server-server-side-performance.md` | 🟠 **YÜKSEK** | 7 kural | Yavaş SSR, API route optimizasyonu, sunucu tarafı şelaleler |
| `4-client-client-side-data-fetching.md` | 🟡 **ORTA-YÜKSEK** | 4 kural | İstemci veri yönetimi, SWR desenleri, tekilleştirme |
| `5-rerender-re-render-optimization.md` | 🟡 **ORTA** | 12 kural | Aşırı yeniden render'lar, React performansı, memoization |
| `6-rendering-rendering-performance.md` | 🟡 **ORTA** | 9 kural | Rendering darboğazları, sanallaştırma, görüntü optimizasyonu |
| `7-js-javascript-performance.md` | ⚪ **DÜŞÜK-ORTA** | 12 kural | Mikro-optimizasyonlar, önbellekleme, döngü performansı |
| `8-advanced-advanced-patterns.md` | 🔵 **DEĞİŞKEN** | 3 kural | Gelişmiş React desenleri, useLatest, init-once |

**Toplam: 8 kategoride 57 kural**

---

## 🚀 Hızlı Karar Ağacı

**Performans sorununuz nedir?**

```
🐌 Yavaş sayfa

 yüklemeleri / Uzun Time to Interactive
  → Bölüm 1 okuyun: Şelaleleri Ortadan Kaldırma
  → Bölüm 2 okuyun: Paket Boyutu Optimizasyonu

📦 Büyük paket boyutu (> 200KB)
  → Bölüm 2 okuyun: Paket Boyutu Optimizasyonu
  → Kontrol edin: Dinamik import'lar, barrel import'lar, tree-shaking

🖥️ Yavaş Sunucu Tarafı Rendering
  → Bölüm 3 okuyun: Sunucu Tarafı Performans
  → Kontrol edin: Paralel veri çekme, streaming

🔄 Çok fazla yeniden render / UI gecikmesi
  → Bölüm 5 okuyun: Yeniden Render Optimizasyonu
  → Kontrol edin: React.memo, useMemo, useCallback

🎨 Rendering performans sorunları
  → Bölüm 6 okuyun: Rendering Performansı
  → Kontrol edin: Sanallaştırma, layout thrashing

🌐 İstemci tarafı veri çekme sorunları
  → Bölüm 4 okuyun: İstemci Tarafı Veri Çekme
  → Kontrol edin: SWR tekilleştirme, localStorage

✨ Gelişmiş desenler gerekli
  → Bölüm 8 okuyun: Gelişmiş Desenler
```

---

## 📊 Etki Öncelik Rehberi

**Kapsamlı optimizasyon yaparken bu sırayı kullanın:**

```
1️⃣ KRİTİK (En Büyük Kazançlar - Önce Yapın):
   ├─ Bölüm 1: Şelaleleri Ortadan Kaldırma
   │  └─ Her şelale tam ağ gecikmesi ekler (100-500ms+)
   └─ Bölüm 2: Paket Boyutu Optimizasyonu
      └─ Time to Interactive ve Largest Contentful Paint'i etkiler

2️⃣ YÜKSEK (Önemli Etki - İkinci Yapın):
   └─ Bölüm 3: Sunucu Taraflı Performans
      └─ Sunucu tarafı şelaleleri ortadan kaldırır, daha hızlı yanıt süreleri

3️⃣ ORTA (Orta Kazançlar - Üçüncü Yapın):
   ├─ Bölüm 4: İstemci Tarafı Veri Çekme
   ├─ Bölüm 5: Yeniden Render Optimizasyonu
   └─ Bölüm 6: Rendering Performansı

4️⃣ DÜŞÜK (Cila - En Son Yapın):
   ├─ Bölüm 7: JavaScript Performansı
   └─ Bölüm 8: Gelişmiş Desenler
```

---

## 🔗 İlgili Yetenekler

| İhtiyaç | Yetenek |
|---------|---------|
| API tasarım desenleri | `@[skills/api-patterns]` |
| Veritabanı optimizasyonu | `@[skills/database-design]` |
| Test stratejileri | `@[skills/testing-patterns]` |
| UI/UX tasarım prensipleri | `@[skills/frontend-design]` |
| TypeScript desenleri | `@[skills/typescript-expert]` |
| Dağıtım ve DevOps | `@[skills/deployment-procedures]` |

---

## ✅ Performans İnceleme Kontrol Listesi

Üretimfiye göndermeden önce:

**Kritik (Mutlaka Düzeltilmeli):**

- [ ] Ardışık veri çekme yok (şelaleler ortadan kaldırıldı)
- [ ] Ana paket için paket boyutu < 200KB
- [ ] Uygulama kodunda barrel import'lar yok
- [ ] Büyük componentler için dinamik import'lar kullanılıyor
- [ ] Mümkün olduğunda paralel veri çekme

**Yüksek Öncelik:**

- [ ] Uygun yerlerde sunucu componentleri kullanıldı
- [ ] API route'lar optimize edildi (N+1 sorgusu yok)
- [ ] Veri çekme için Suspense sınırları
- [ ] Mümkün olduğunda statik oluşturma kullanıldı

**Orta Öncelik:**

- [ ] Pahalı hesaplamalar memoize edildi
- [ ] Liste rendering sanallaştırıldı (> 100 öğe ise)
- [ ] Görseller next/image ile optimize edildi
- [ ] Gereksiz yeniden render yok

**Düşük Öncelik (Cila):**

- [ ] Sık kullanılan yol (hot path) döngüleri optimize edildi
- [ ] RegExp desenleri yukarı taşındı (hoisted)
- [ ] Döngülerde özellik erişimi önbelleğe alındı

---

## ❌ Anti-Desenler (Yaygın Hatalar)

**YAPMAYIN:**

- ❌ Bağımsız işlemler için ardışık `await` kullanmak
- ❌ Bir fonksiyona ihtiyacınız varken tüm kütüphaneyi import etmek
- ❌ Uygulama kodunda barrel export'lar (`index.ts` re-export'ları) kullanmak
- ❌ Büyük componentler/kütüphaneler için dinamik import'ları atlamak
- ❌ useEffect'te tekilleştirme olmadan veri çekmek
- ❌ Pahalı hesaplamaları memoize etmeyi unutmak
- ❌ Sunucu componentleri işe yararken istemci componentleri kullanmak

**YAPIN:**

- ✅ `Promise.all()` ile paralel veri çekin
- ✅ Dinamik import'lar kullanın: `const Comp = dynamic(() => import('./Heavy'))`
- ✅ Doğrudan import edin: `import { specific } from 'library/specific'`
- ✅ Daha iyi UX için Suspense sınırları kullanın
- ✅ React Server Components'ten yararlanın
- ✅ Optimize etmeden önce performansı ölçün
- ✅ Next.js yerleşik optimizasyonlarını kullanın (next/image, next/font)

---

## 🎯 Bu Yetenek Nasıl Kullanılır

### Yeni Özellikler İçin:

1. İnşa ederken **Bölüm 1 ve 2'yi** kontrol edin (şelaleleri önleyin, paketi küçük tutun)
2. Varsayılan olarak sunucu componentlerini kullanın (Bölüm 3)
3. Pahalı işlemler için memoization uygulayın (Bölüm 5)

### Performans İncelemeleri İçin:

1. **Bölüm 1** ile başlayın (şelaleler = en büyük etki)
2. Sonra **Bölüm 2** (paket boyutu)
3. Sonra **Bölüm 3** (sunucu tarafı)
4. Son olarak gerektiğinde diğer bölümler

### Yavaş Performansı Debug Etmek İçin:

1. Semptom tanımlayın (yavaş yükleme, gecikme, vb.)
2. Yukarıdaki Hızlı Karar Ağacı'nı kullanın
3. İlgili bölümü okuyun
4. Düzeltmeleri öncelik sırasına göre uygulayın

---

## 📚 Öğrenme Yolu

**Başlangıç (Kritik'e Odaklanın):**
→ Bölüm 1: Şelaleleri Ortadan Kaldırma
→ Bölüm 2: Paket Boyutu Optimizasyonu

**Orta Seviye (Yüksek Öncelik Ekleyin):**
→ Bölüm 3: Sunucu Tarafı Performans
→ Bölüm 5: Yeniden Render Optimizasyonu

**İleri Seviye (Tam Optimizasyon):**
→ Tüm bölümler + Bölüm 8: Gelişmiş Desenler

---

## 🔍 Doğrulama Scripti

| Script | Amaç | Komut |
|--------|------|-------|
| `scripts/react_performance_checker.py` | Otomatik performans denetimi | `python scripts/react_performance_checker.py <proje_yolu>` |

---

## 📖 Bölüm Detayları

### Bölüm 1: Şelaleleri Ortadan Kaldırma (KRİTİK)

**Etki:** Her şelale 100-500ms+ gecikme ekler
**Temel Kavramlar:** Paralel çekme, Promise.all(), Suspense sınırları, preloading

### Bölüm 2: Paket Boyutu Optimizasyonu (KRİTİK)

**Etki:** Time to Interactive, Largest Contentful Paint'i doğrudan etkiler
**Temel Kavramlar:** Dinamik import'lar, tree-shaking, barrel import'tan kaçınma

### Bölüm 3: Sunucu Tarafı Performans (YÜKSEK)

**Etki:** Daha hızlı sunucu yanıtları, daha iyi SEO
**Temel Kavramlar:** Paralel sunucu çekme, streaming, API route optimizasyonu

### Bölüm 4: İstemci Tarafı Veri Çekme (ORTA-YÜKSEK)

**Etki:** Gereksiz istekleri azaltır, daha iyi UX
**Temel Kavramlar:** SWR tekilleştirme, localStorage önbellekleme, event listener'lar

### Bölüm 5: Yeniden Render Optimizasyonu (ORTA)

**Etki:** Daha akıcı UI, daha az boşa giden hesaplama
**Temel Kavramlar:** React.memo, useMemo, useCallback, component yapısı

### Bölüm 6: Rendering Performansı (ORTA)

**Etki:** Daha iyi rendering verimliliği
**Temel Kavramlar:** Sanallaştırma, görüntü optimizasyonu, layout thrashing

### Bölüm 7: JavaScript Performansı (DÜŞÜK-ORTA)

**Etki:** Sık kullanılan yollarda (hot paths) kademeli iyileştirmeler
**Temel Kavramlar:** Döngü optimizasyonu, önbellekleme, RegExp yukarı taşıma

### Bölüm 8: Gelişmiş Desenler (DEĞİŞKEN)

**Etki:** Özel kullanım durumları
**Temel Kavramlar:** useLatest hook, init-once desenleri, event handler ref'ler

---

## 🎓 En İyi Pratikler Özeti

**Altın Kurallar:**

1. **Önce ölçün** - React DevTools Profiler, Chrome DevTools kullanın
2. **En büyük etki önce** - Şelaleler → Paket → Sunucu → Mikro
3. **Aşırı optimize etmeyin** - Gerçek darboğazlara odaklanın
4. **Platform özelliklerini kullanın** - Next.js'te yerleşik optimizasyonlar var
5. **Kullanıcıları düşünün** - Gerçek dünya koşulları önemlidir

**Performans Zihniyeti:**

- Ardışıktaki her `await` = potansiyel şelale
- Her `import` = potansiyel paket şişmesi
- Her yeniden render = (gereksizse) boşa giden hesaplama
- Sunucu componentleri = daha az gönderilecek JavaScript
- Tahmin etmeyin, ölçün

---

**Kaynak:** Vercel Mühendisliği
**Tarih:** Ocak 2026
**Versiyon:** 1.0.0
**Toplam Kural:** 8 kategoride 57 kural
