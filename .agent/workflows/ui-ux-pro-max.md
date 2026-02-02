---
description: Kullanıcı Arayüzü (UI) planlayın ve uygulayın
---

---
description: 50+ stil, 95+ renk paleti ve otomatik tasarım sistemi oluşturma özelliğine sahip YZ destekli tasarım zekası
---

# ui-ux-pro-max

Web ve mobil uygulamalar için kapsamlı tasarım kılavuzu. 9 teknoloji yığını genelinde 50+ stil, 97 renk paleti, 57 font eşleşmesi, 99 UX yönergesi ve 25 grafik türü içerir. Öncelik tabanlı önerilere sahip aranabilir bir veritabanıdır.

## Ön Koşullar

Python'un kurulu olup olmadığını kontrol edin:

```bash
python3 --version || python --version
```

Python kurulu değilse, kullanıcının işletim sistemine göre kurun:

**macOS:**
```bash
brew install python3
```

**Ubuntu/Debian:**
```bash
sudo apt update && sudo apt install python3
```

**Windows:**
```powershell
winget install Python.Python.3.12
```

---

## Bu İş Akışı Nasıl Kullanılır?

Kullanıcı UI/UX çalışması (tasarım, oluşturma, uygulama, inceleme, düzeltme, iyileştirme) talep ettiğinde bu iş akışını takip edin:

### 1. Adım: Kullanıcı Gereksinimlerini Analiz Et

Kullanıcı isteğinden temel bilgileri çıkarın:
- **Ürün türü**: SaaS, e-ticaret, portföy, panel (dashboard), açılış sayfası (landing page), vb.
- **Stil anahtar kelimeleri**: minimal, oyuncu, profesyonel, zarif, karanlık mod, vb.
- **Sektör**: sağlık, fintech, oyun, eğitim, vb.
- **Teknoloji Yığını (Stack)**: React, Vue, Next.js veya varsayılan olarak `html-tailwind`

### 2. Adım: Tasarım Sistemi Oluştur (ZORUNLU)

Gerekçelendirilmiş kapsamlı öneriler almak için **her zaman `--design-system` ile başlayın**:

```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "<urun_turu> <sektor> <anahtar_kelimeler>" --design-system [-p "Proje Adı"]
```

Bu komut:
1. 5 alanı (domain) paralel olarak arar (ürün, stil, renk, sayfa yapısı, tipografi)
2. En iyi eşleşmeleri seçmek için `ui-reasoning.csv` dosyasındaki mantık kurallarını uygular
3. Tam tasarım sistemini döndürür: desen, stil, renkler, tipografi, efektler
4. Kaçınılması gereken anti-desenleri (anti-patterns) içerir

**Örnek:**
```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "güzellik spa sağlık hizmeti" --design-system -p "Serenity Spa"
```

### 2b. Adım: Tasarım Sistemini Kalıcı Hale Getir (Ana + Geçersiz Kılma Deseni)

Tasarım sistemini oturumlar arası hiyerarşik erişim için kaydetmek üzere `--persist` ekleyin:

```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "<sorgu>" --design-system --persist -p "Proje Adı"
```

Bu şunları oluşturur:
- `design-system/MASTER.md` — Tüm tasarım kurallarını içeren Global Doğruluk Kaynağı
- `design-system/pages/` — Sayfaya özgü geçersiz kılmalar (overrides) için klasör

**Sayfaya özgü geçersiz kılma ile:**
```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "<sorgu>" --design-system --persist -p "Proje Adı" --page "dashboard"
```

Bu ayrıca şunları oluşturur:
- `design-system/pages/dashboard.md` — Ana dosyadan (Master) sayfaya özgü sapmalar

**Hiyerarşik erişim nasıl çalışır:**
1. Belirli bir sayfayı oluştururken (örneğin "Ödeme"), önce `design-system/pages/odeme.md` dosyasını kontrol edin
2. Sayfa dosyası mevcutsa, kuralları Ana (Master) dosyayı **geçersiz kılar**
3. Mevcut değilse, sadece `design-system/MASTER.md` dosyasını kullanın

### 3. Adım: Detaylı Aramalarla Destekle (gerektiğinde)

Tasarım sistemini aldıktan sonra, ek detaylar için alan (domain) aramalarını kullanın:

```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "<anahtar_kelime>" --domain <alan> [-n <maks_sonuc>]
```

**Ne zaman detaylı arama yapılmalı:**

| İhtiyaç | Alan | Örnek |
|------|--------|---------|
| Daha fazla stil seçeneği | `style` | `--domain style "glassmorphism dark"` |
| Grafik önerileri | `chart` | `--domain chart "gerçek zamanlı panel"` |
| UX en iyi pratikleri | `ux` | `--domain ux "animasyon erişilebilirlik"` |
| Alternatif yazı tipleri | `typography` | `--domain typography "zarif lüks"` |
| Sayfa yapısı | `landing` | `--domain landing "hero sosyal-kanıt"` |

### 4. Adım: Yazılım Yığını Kılavuzları (Varsayılan: html-tailwind)

Uygulamaya özel en iyi pratikleri alın. Kullanıcı bir yığın belirtmezse, **varsayılan olarak `html-tailwind` kullanın**.

```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "<anahtar_kelime>" --stack html-tailwind
```

Kullanılabilir yığınlar (stacks): `html-tailwind`, `react`, `nextjs`, `vue`, `svelte`, `swiftui`, `react-native`, `flutter`, `shadcn`, `jetpack-compose`

---

## Arama Referansı

### Kullanılabilir Alanlar (Domains)

| Alan | Kullanım Amacı | Örnek Anahtar Kelimeler |
|--------|---------|------------------|
| `product` | Ürün türü önerileri | SaaS, e-ticaret, portföy, sağlık, güzellik, hizmet |
| `style` | UI stilleri, renkler, efektler | glassmorphism, minimalizm, karanlık mod, brutalizm |
| `typography` | Yazı tipi eşleşmeleri, Google Fonts | zarif, oyuncu, profesyonel, modern |
| `color` | Ürün türüne göre renk paletleri | saas, e-ticaret, sağlık, güzellik, fintech, hizmet |
| `landing` | Sayfa yapısı, CTA stratejileri | hero, hero-odaklı, referans, fiyatlandırma, sosyal-kanıt |
| `chart` | Grafik türleri, kütüphane önerileri | trend, karşılaştırma, zaman çizelgesi, huni, pasta |
| `ux` | En iyi pratikler, anti-desenler | animasyon, erişilebilirlik, z-index, yükleme |
| `react` | React/Next.js performansı | waterfall, bundle, suspense, memo, rerender, cache |
| `web` | Web arayüzü yönergeleri | aria, odak, klavye, semantik, sanallaştırma |
| `prompt` | YZ komutları, CSS anahtar kelimeleri | (stil adı) |

### Kullanılabilir Yazılım Yığınları (Stacks)

| Yığın (Stack) | Odak Noktası |
|-------|-------|
| `html-tailwind` | Tailwind yardımcı sınıfları, responsive, a11y (VARSIYILAN) |
| `react` | Durum (state), hook'lar, performans, desenler |
| `nextjs` | SSR, yönlendirme, görseller, API rotaları |
| `vue` | Composition API, Pinia, Vue Router |
| `svelte` | Runes, depolar (stores), SvelteKit |
| `swiftui` | Görünümler (Views), Durum, Navigasyon, Animasyon |
| `react-native` | Bileşenler, Navigasyon, Listeler |
| `flutter` | Widget'lar, Durum, Düzen, Temalandırma |
| `shadcn` | shadcn/ui bileşenleri, temalandırma, formlar, desenler |
| `jetpack-compose` | Birleştirilebilir öğeler (Composables), Değiştiriciler (Modifiers), Durum Yönetimi |

---

## Örnek İş Akışı

**Kullanıcı isteği:** "Profesyonel bir cilt bakımı hizmeti için açılış sayfası yap"

### 1. Adım: Gereksinimleri Analiz Et
- Ürün türü: Güzellik/Spa hizmeti
- Stil anahtar kelimeleri: zarif, profesyonel, yumuşak
- Sektör: Güzellik/Sağlık
- Yazılım Yığını: html-tailwind (varsayılan)

### 2. Adım: Tasarım Sistemi Oluştur (ZORUNLU)

```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "beauty spa wellness service elegant" --design-system -p "Serenity Spa"
```

**Çıktı:** Desen, stil, renkler, tipografi, efektler ve anti-desenleri içeren tam tasarım sistemi.

### 3. Adım: Detaylı Aramalarla Destekle (gerektiğinde)

```bash
# Animasyon ve erişilebilirlik için UX yönergelerini al
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "animation accessibility" --domain ux

# Gerekirse alternatif tipografi seçeneklerini al
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "elegant luxury serif" --domain typography
```

### 4. Adım: Yazılım Yığını Kılavuzları

```bash
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "layout responsive form" --stack html-tailwind
```

**Ardından:** Tasarım sistemi + detaylı aramaları sentezleyin ve tasarımı uygulayın.

---

## Çıktı Formatları

`--design-system` bayrağı iki çıktı formatını destekler:

```bash
# ASCII kutu (varsayılan) - terminal ekranı için en iyisi
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "fintech crypto" --design-system

# Markdown - dokümantasyon için en iyisi
python3 .agent/.shared/ui-ux-pro-max/scripts/search.py "fintech crypto" --design-system -f markdown
```

---

## Daha İyi Sonuçlar İçin İpuçları

1. **Anahtar kelimelerde spesifik olun** - "sağlık SaaS paneli" > "uygulama"
2. **Birden fazla kez arayın** - Farklı anahtar kelimeler farklı içgörüler sunar
3. **Alanları birleştirin** - Stil + Tipografi + Renk = Tam tasarım sistemi
4. **Her zaman UX'i kontrol edin** - Yaygın sorunlar için "animasyon", "z-index", "erişilebilirlik" araması yapın
5. **Yığın (stack) bayrağını kullanın** - Uygulamaya özel en iyi pratikleri alın
6. **Yineleyin** - İlk arama eşleşmezse farklı anahtar kelimeler deneyin

---

## Profesyonel UI İçin Ortak Kurallar

Bunlar, UI'ın profesyonel görünmemesine neden olan ve sıkça gözden kaçan sorunlardır:

### İkonlar ve Görsel Öğeler

| Kural | Yap | Yapma |
|------|----|----- |
| **Emoji ikon yok** | SVG ikonları kullan (Heroicons, Lucide, Simple Icons) | UI ikonu olarak 🎨 🚀 ⚙️ gibi emojiler kullanma |
| **Kararlı hover durumları** | Üzerine gelindiğinde (hover) renk/opaklık geçişleri kullan | Düzeni kaydıran ölçeklendirme (scale) dönüşümleri yapma |
| **Doğru marka logoları** | Simple Icons'dan resmi SVG'leri araştır | Yanlış logo yollarını tahmin etme veya kullanma |
| **Tutarlı ikon boyutları** | w-6 h-6 ile sabit viewBox (24x24) kullan | Farklı ikon boyutlarını rastgele karıştırma |

### Etkileşim ve İmleç

| Kural | Yap | Yapma |
|------|----|----- |
| **İmleç göstergesi (pointer)** | Tüm tıklanabilir/hover edilebilir kartlara `cursor-pointer` ekle | Etkileşimli öğelerde varsayılan imleci bırakma |
| **Hover geri bildirimi** | Görsel geri bildirim sağla (renk, gölge, kenarlık) | Öğenin etkileşimli olduğuna dair hiçbir belirti bırakmama |
| **Pürüzsüz geçişler** | `transition-colors duration-200` kullan | Anında durum değişiklikleri veya çok yavaş (>500ms) geçişler |

### Işık/Karanlık Mod Kontrastı

| Kural | Yap | Yapma |
|------|----|----- |
| **İyi ışık modu cam kartı** | `bg-white/80` veya daha yüksek opaklık kullan | `bg-white/10` kullanma (çok şeffaf kalır) |
| **Işık modu metin kontrastı** | Metin için `#0F172A` (slate-900) kullan | Gövde metni için `#94A3B8` (slate-400) kullanma |
| **Işık modu silik metin** | Minimum `#475569` (slate-600) kullan | gray-400 veya daha açık renkleri kullanma |
| **Kenarlık görünürlüğü** | Işık modunda `border-gray-200` kullan | `border-white/10` kullanma (görünmez kalır) |

### Düzen ve Boşluklandırma

| Kural | Yap | Yapma |
|------|----|----- |
| **Yüzen navbar** | `top-4 left-4 right-4` boşluğu ekle | Navigasyon çubuğunu doğrudan `top-0` sınırına yapıştırma |
| **İçerik dolgusu (padding)** | Sabit navbar yüksekliğini hesaba kat | İçeriğin sabit öğelerin arkasında kalmasına izin verme |
| **Tutarlı maksimum genişlik** | Aynı `max-w-6xl` veya `max-w-7xl` değerini kullan | Farklı konteyner genişliklerini karıştırma |

---

## Teslim Öncesi Kontrol Listesi

UI kodunu teslim etmeden önce bu maddeleri doğrulayın:

### Görsel Kalite
- [ ] İkon olarak emoji kullanılmadı (yerine SVG kullanıldı)
- [ ] Tüm ikonlar tutarlı bir setten (Heroicons/Lucide)
- [ ] Marka logoları doğru (Simple Icons'dan doğrulandı)
- [ ] Hover durumları düzen kaymasına (layout shift) neden olmuyor
- [ ] var() sarmalayıcısı yerine doğrudan tema renklerini (bg-primary) kullanın

### Etkileşim
- [ ] Tüm tıklanabilir öğelerde `cursor-pointer` mevcut
- [ ] Hover durumları net görsel geri bildirim sağlıyor
- [ ] Geçişler pürüzsüz (150-300ms)
- [ ] Klavye navigasyonu için odak (focus) durumları görünür

### Işık/Karanlık Mod
- [ ] Işık modu metni yeterli kontrasta sahip (minimum 4.5:1)
- [ ] Cam/şeffaf öğeler ışık modunda görünür
- [ ] Kenarlıklar her iki modda da görünür
- [ ] Teslim etmeden önce her iki modu da test edin

### Düzen (Layout)
- [ ] Yüzen öğelerin kenarlardan uygun boşlukları var
- [ ] Sabit navbar'ların arkasında gizli içerik yok
- [ ] 375px, 768px, 1024px, 1440px genişliklerinde uyumlu (responsive)
- [ ] Mobilde yatay kaydırma (horizontal scroll) yok

### Erişilebilirlik
- [ ] Tüm görsellerin alt metni (alt text) var
- [ ] Form alanlarının etiketleri (labels) var
- [ ] Renk, tek gösterge değil
- [ ] `prefers-reduced-motion` ayarına saygı duyuldu