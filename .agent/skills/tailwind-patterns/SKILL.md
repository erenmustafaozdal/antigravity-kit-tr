---
name: tailwind-patterns
description: Tailwind CSS v4 prensipleri. CSS-öncelikli yapılandırma, container sorguları, modern desenler, tasarım token mimarisi.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# Tailwind CSS Desenleri (v4 - 2025)

> CSS-native yapılandırma ile modern utility-first CSS.

---

## 1. Tailwind v4 Mimarisi

### v3'ten Ne Değişti

| v3 (Eski) | v4 (Güncel) |
|-----------|-------------|
| `tailwind.config.js` | CSS-tabanlı `@theme` direktifi |
| PostCSS eklentisi | Oxide motoru (10x daha hızlı) |
| JIT modu | Native, her zaman açık |
| Plugin sistemi | CSS-native özellikler |
| `@apply` direktifi | Hala çalışır, önerilmez |

### v4 Temel Kavramlar

| Kavram | Açıklama |
|--------|----------|
| **CSS-öncelikli** | JavaScript değil CSS'de yapılandırma |
| **Oxide Motoru** | Rust-tabanlı derleyici, çok daha hızlı |
| **Native İç içe Geçme** | PostCSS olmadan CSS nesting |
| **CSS Değişkenleri** | Tüm tokenler `--*` değişkenleri olarak açığa çıkar |

---

## 2. CSS-Tabanlı Yapılandırma

### Theme Tanımı

```
@theme {
  /* Renkler - anlam yüklü isimler kullan */
  --color-primary: oklch(0.7 0.15 250);
  --color-surface: oklch(0.98 0 0);
  --color-surface-dark: oklch(0.15 0 0);
  
  /* Spacing ölçeği */
  --spacing-xs: 0.25rem;
  --spacing-sm: 0.5rem;
  --spacing-md: 1rem;
  --spacing-lg: 2rem;
  
  /* Tipografi */
  --font-sans: 'Inter', system-ui, sans-serif;
  --font-mono: 'JetBrains Mono', monospace;
}
```

### Ne Zaman Genişletmeli vs Üzerine Yazmalı

| Eylem | Ne Zaman Kullanılır |
|-------|---------------------|
| **Genişlet** | Varsayılanlarla birlikte yeni değerler eklerken |
| **Üzerine Yaz** | Varsayılan ölçeği tamamen değiştirirken |
| **Anlam yüklü tokenler** | Projeye özgü isimlendirme (primary, surface) |

---

## 3. Container Sorguları (v4 Native)

### Breakpoint vs Container

| Tip | Neye Yanıt Verir |
|-----|------------------|
| **Breakpoint** (`md:`) | Viewport genişliği |
| **Container** (`@container`) | Ebeveyn element genişliği |

### Container Sorgusu Kullanımı

| Desen | Sınıflar |
|-------|----------|
| Container tanımla | Ebeveyne `@container` |
| Container breakpoint | Çocuklara `@sm:`, `@md:`, `@lg:` |
| İsimlendirilmiş containerlar | Özellik için `@container/card` |

### Ne Zaman Kullanılır

| Senaryo | Kullanım |
|---------|----------|
| Sayfa düzeyi düzenler | Viewport breakpointleri |
| Component düzeyi responsive | Container sorguları |
| Yeniden kullanılabilir componentler | Container sorguları (bağlamdan bağımsız) |

---

## 4. Responsive Tasarım

### Breakpoint Sistemi

| Prefix | Min Genişlik | Hedef |
|--------|--------------|-------|
| (yok) | 0px | Mobil-öncelikli temel |
| `sm:` | 640px | Büyük telefon / küçük tablet |
| `md:` | 768px | Tablet |
| `lg:` | 1024px | Laptop |
| `xl:` | 1280px | Masaüstü |
| `2xl:` | 1536px | Büyük masaüstü |

### Mobil-Öncelikli Prensip

1. Önce mobil stilleri yaz (prefix yok)
2. Daha büyük ekranlar için prefix'li geçersiz kılmalar ekle
3. Örnek: `w-full md:w-1/2 lg:w-1/3`

---

## 5. Dark Mode

### Yapılandırma Stratejileri

| Metod | Davranış | Ne Zaman Kullanılır |
|-------|----------|---------------------|
| `class` | `.dark` sınıfı açıp kapatır | Manuel tema değiştiricisi |
| `media` | Sistem tercihini takip eder | Kullanıcı kontrolü yok |
| `selector` | Özel seçici (v4) | Karmaşık temalama |

### Dark Mode Deseni

| Element | Açık | Koyu |
|---------|------|------|
| Arka plan | `bg-white` | `dark:bg-zinc-900` |
| Metin | `text-zinc-900` | `dark:text-zinc-100` |
| Kenarlıklar | `border-zinc-200` | `dark:border-zinc-700` |

---

## 6. Modern Düzen Desenleri

### Flexbox Desenleri

| Desen | Sınıflar |
|-------|----------|
| Merkez (her iki eksen) | `flex items-center justify-center` |
| Dikey yığın | `flex flex-col gap-4` |
| Yatay sıra | `flex gap-4` |
| Aralarında boşluk | `flex justify-between items-center` |
| Sarmalayan grid | `flex flex-wrap gap-4` |

### Grid Desenleri

| Desen | Sınıflar |
|-------|----------|
| Otomatik sığdırma responsive | `grid grid-cols-[repeat(auto-fit,minmax(250px,1fr))]` |
| Asimetrik (Bento) | `grid grid-cols-3 grid-rows-2` with spans |
| Kenar çubuğu düzeni | `grid grid-cols-[auto_1fr]` |

> **Not:** Simetrik 3 sütunlu gridlerden ziyade asimetrik/Bento düzenleri tercih edin.

---

## 7. Modern Renk Sistemi

### OKLCH vs RGB/HSL

| Format | Avantaj |
|--------|---------|
| **OKLCH** | Algısal olarak düzgün, tasarım için daha iyi |
| **HSL** | Sezgisel ton/doygunluk |
| **RGB** | Eski uyumluluk |

### Renk Token Mimarisi

| Katman | Örnek | Amaç |
|--------|-------|------|
| **İlkel** | `--blue-500` | Ham renk değerleri |
| **Anlam yüklü** | `--color-primary` | Amaca dayalı isimlendirme |
| **Component** | `--button-bg` | Component'e özgü |

---

## 8. Tipografi Sistemi

### Font Stack Deseni

| Tip | Önerilen |
|-----|----------|
| Sans | `'Inter', 'SF Pro', system-ui, sans-serif` |
| Mono | `'JetBrains Mono', 'Fira Code', monospace` |
| Display | `'Outfit', 'Poppins', sans-serif` |

### Tip Ölçeği

| Sınıf | Boyut | Kullanım |
|-------|-------|----------|
| `text-xs` | 0.75rem | Etiketler, açıklamalar |
| `text-sm` | 0.875rem | İkincil metin |
| `text-base` | 1rem | Gövde metni |
| `text-lg` | 1.125rem | Öne çıkan metin |
| `text-xl`+ | 1.25rem+ | Başlıklar |

---

## 9. Animasyon & Geçişler

### Yerleşik Animasyonlar

| Sınıf | Efekt |
|-------|-------|
| `animate-spin` | Sürekli dönüş |
| `animate-ping` | Dikkat nabzı |
| `animate-pulse` | Hafif opaklık nabzı |
| `animate-bounce` | Zıplama efekti |

### Geçiş Desenleri

| Desen | Sınıflar |
|-------|----------|
| Tüm özellikler | `transition-all duration-200` |
| Belirli | `transition-colors duration-150` |
| Easing ile | `ease-out` veya `ease-in-out` |
| Hover efekti | `hover:scale-105 transition-transform` |

---

## 10. Component Çıkarma

### Ne Zaman Çıkarmalı

| Sinyal | Eylem |
|--------|-------|
| Aynı sınıf kombinasyonu 3+ kez | Component çıkar |
| Karmaşık durum varyantları | Component çıkar |
| Tasarım sistemi elementi | Çıkar + belgele |

### Çıkarma Metodları

| Metod | Ne Zaman Kullanılır |
|-------|---------------------|
| **React/Vue component** | Dinamik, JS gerekli |
| **CSS'de @apply** | Statik, JS gerekmiyor |
| **Tasarım tokenları** | Yeniden kullanılabilir değerler |

---

## 11. Anti-Desenler

| Yapma | Yap |
|-------|-----|
| Her yerde keyfi değerler | Tasarım sistemi ölçeği kullan |
| `!important` | Specificity'yi düzgün düzelt |
| Inline `style=` | Utility'leri kullan |
| Uzun sınıf listelerini kopyala | Component çıkar |
| v3 config'i v4 ile karıştır | Tamamen CSS-öncelikli'ye geç |
| `@apply`'ı yoğun kullan | Componentleri tercih et |

---

## 12. Performans Prensipleri

| Prensip | Implementasyon |
|---------|----------------|
| **Kullanılmayanları temizle** | v4'te otomatik |
| **Dinamizmden kaçın** | Template string sınıflar yok |
| **Oxide Kullan** | v4'te varsayılan, 10x daha hızlı |
| **Build'leri önbelleğe al** | CI/CD önbellekleme |

---

> **Unutma:** Tailwind v4 CSS-önceliklidir. CSS değişkenlerini, container sorgularını ve native özellikleri benimseyin. Config dosyası artık opsiyonel.
