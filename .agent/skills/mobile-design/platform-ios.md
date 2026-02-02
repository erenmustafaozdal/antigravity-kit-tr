# iOS Platform Yönergeleri

> İnsan Arayüzü Yönergeleri (HIG) temelleri, iOS tasarım kuralları, SF Pro tipografisi ve yerel (native) desenler.
> **iPhone/iPad için geliştirme yaparken bu dosyayı okuyun.**

---

## 1. İnsan Arayüzü Yönergeleri (HIG) Felsefesi

### Temel Apple Tasarım Prensipleri

```
NETLİK (CLARITY):
├── Metin her boyutta okunabilir
├── İkonlar kesin ve anlaşılır
├── Süslemeler ölçülü ve amaca uygun
└── Tasarımı işlevsellik odağı yönlendirir

SAYGI (DEFERENCE):
├── UI, insanların anlamasına ve etkileşime girmesine yardımcı olur
├── İçerik ekranı doldurur
├── UI asla içerikle rekabet etmez
└── Geçirgenlik (translucency), daha fazla içeriğe dair ipucu verir

DERİNLİK (DEPTH):
├── Belirgin görsel katmanlar hiyerarşiyi iletir
├── Geçişler derinlik hissi sağlar
├── Dokunma, işlevselliği ortaya çıkarır
└── İçerik, UI'dan daha ön plandadır
```

### iOS Tasarım Değerleri

| Değer | Uygulama |
|-------|----------------|
| **Estetik Bütünlük** | Tasarım işleviyle örtüşür (oyun ≠ verimlilik) |
| **Tutarlılık** | Sistem kontrollerini ve tanıdık desenleri kullanın |
| **Doğrudan Manipülasyon** | Dokunma, içeriği doğrudan etkiler |
| **Geri Bildirim** | Eylemler onaylanır ve yanıtlanır |
| **Metaforlar** | Gerçek dünya benzetmeleri anlamayı kolaylaştırır |
| **Kullanıcı Kontrolü** | Eylemleri kullanıcı başlatır ve iptal edebilir |

---

## 2. iOS Tipografisi

### SF Pro Yazı Tipi Ailesi

```
iOS Sistem Yazı Tipleri:
├── SF Pro Text: Gövde metni (< 20pt)
├── SF Pro Display: Büyük başlıklar (≥ 20pt)
├── SF Pro Rounded: Arkadaş canlısı bağlamlar
├── SF Mono: Kod, tablosal veriler
└── SF Compact: Apple Watch, küçük ekranlar
```

### iOS Yazı Tipi Ölçeği (Dynamic Type)

| Stil | Varsayılan Boyut | Kalınlık | Kullanım |
|-------|--------------|--------|-------|
| **Large Title** | 34pt | Bold | Navigasyon çubuğu (kaydırınca küçülen) |
| **Title 1** | 28pt | Bold | Sayfa başlıkları |
| **Title 2** | 22pt | Bold | Bölüm başlıkları |
| **Title 3** | 20pt | Semibold | Alt bölüm başlıkları |
| **Headline** | 17pt | Semibold | Vurgulanmış gövde metni |
| **Body** | 17pt | Regular | Birincil içerik |
| **Callout** | 16pt | Regular | İkincil içerik |
| **Subhead** | 15pt | Regular | Üçüncül içerik |

> 🔴 **ZORUNLU:** Kullanıcı yazı tipi ayarına göre ölçeklenen Dynamic Type desteğini HER ZAMAN sağlayın.

---

## 3. iOS Renk Sistemi

### Semantik (Anlamsal) Renkler

```
Karanlık mod için semantik renkleri kullanın:

Birincil:
├── .label → Birincil metin
├── .secondaryLabel → İkincil metin
├── .tertiaryLabel → Üçüncül metin

Arka Planlar:
├── .systemBackground → Ana arka plan
├── .secondarySystemBackground → Gruplanmış içerik
├── .tertiarySystemBackground → Yükseltilmiş içerik
```

---

## 4. iOS Düzen ve Boşluklar (Layout & Spacing)

### Güvenli Alanlar (Safe Areas)

```
┌─────────────────────────────────────┐
│░░░░░░░░░░ Durum Çubuğu ░░░░░░░░░░░░░│ ← Üst güvenli alan boşluğu
├─────────────────────────────────────┤
│                                     │
│         Güvenli İçerik Alanı        │
│                                     │
├─────────────────────────────────────┤
│░░░░░░░░ Ana Ekran Çubuğu ░░░░░░░░░░│ ← Alt güvenli alan boşluğu
└─────────────────────────────────────┘

KURAL: Etkileşimli içeriği asla güvensiz alanlara yerleştirmeyin.
```

| Öğe | Boşluk | Notlar |
|---------|--------|-------|
| Ekran kenarı → içerik | 16pt | Standart yatay kenar boşluğu |
| Liste öğesi dolgusu | 16pt yatay | Standart hücre dolgusu |
| Buton iç dolgusu | 12pt dikey, 16pt yatay | Minimum öneri |

---

## 5. iOS Navigasyon Desenleri

### Navigasyon Türleri

| Desen | Kullanım Durumu | Uygulama |
|---------|----------|----------------|
| **Tab Bar** | 3-5 ana bölüm | Alt kısım, her zaman görünür |
| **Navigasyon Denetleyicisi**| Hiyerarşik derinleşme | Stack tabanlı, geri butonu |
| **Modal** | Odaklanmış görev | Sayfa (sheet) veya tam ekran |

### Tab Bar Kuralları

- **3-5 öğe** maksimum.
- **İkonlar:** SF Symbols veya özel ikonlar (25x25pt).
- **Etiketler:** Erişilebilirlik için her zaman ekleyin.
- **Aktif Durum:** Dolgulu ikon + vurgu rengi.

---

## 6. iOS Bileşenleri

### Listeler ve Tablolar

- **.insetGrouped:** Yuvarlatılmış kartlar (iOS 14+ varsayılanı).
- ** Disclosure indicator (>):** Detay sayfasına gider.
- ** Checkmark (✓):** Seçim durumu.

---

## 7. iOS-Özgü Desenler

### Çek-Yenile (Pull to Refresh)
SADECE yerel `UIRefreshControl` davranışını kullanın; özel yapılar inşa etmekten kaçının.

### Kaydırma (Swipe) Eylemleri
- **Soldan Sağa kaydırma:** Genellikle birincil eylemi (örneğin Pinleme) tetikler.
- **Sağdan Sola kaydırma:** Silme, Arşivleme gibi eylemleri gösterir.

### Bağlam Menüleri (Context Menus)
Uzun basış ile açılan, içerikle ilgili eylemleri ve önizlemeyi içeren menülerdir.

---

## 8. SF Symbols
Apple'ın 5000'den fazla ikondan oluşan kütüphanesidir. Metin ağırlığı ile ikon ağırlığını her zaman eşleştirin (örneğin metin bold ise ikon da bold olmalı).

---

## 9. iOS Erişilebilirlik (Accessibility)

- **VoiceOver:** Her etkileşimli öğeye `accessibilityLabel` ekleyin.
- **Dynamic Type:** Yazı tipi boyutunun xSmall'dan xxxLarge'a (ve daha ötesine) kadar ölçeklenebildiğinden emin olun.
- **Hareketi Azalt (Reduce Motion):** Kullanıcının sistem tercihlerine göre animasyonları optimize edin.

---

## 10. iOS Kontrol Listesi

- [ ] **SF Pro ve SF Symbols kullanılıyor mu?**
- [ ] **Dynamic Type destekleniyor mu?**
- [ ] **Güvenli alanlara (Safe Areas) uyuluyor mu?**
- [ ] **Geri gitme jesti (edge swipe) çalışıyor mu?**
- [ ] **Dokunmatik hedefler ≥ 44pt mi?**
- [ ] **Karanlık mod test edildi mi?**
- [ ] **Klavye kaçınma (keyboard avoidance) uygulandı mı?**

---

> **Unutma:** iOS kullanıcılarının diğer iOS uygulamalarından gelen güçlü beklentileri vardır. HIG desenlerinden sapmak onlara "bozuk" hissettirir. Şüpheye düştüğünüzde, yerel bileşeni kullanın.
