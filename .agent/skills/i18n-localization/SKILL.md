---
name: i18n-localization
description: Uluslararasılaştırma (i18n) ve yerelleştirme (L10n) desenleri. Hardcoded metinleri belirleme, çevirileri yönetme, yerel ayar dosyaları, Sağdan Sola (RTL) desteği.
allowed-tools: Read, Glob, Grep
---

# i18n ve Yerelleştirme (Localization)

> Uluslararasılaştırma (i18n) ve Yerelleştirme (L10n) için en iyi pratikler.

---

## 1. Temel Kavramlar

| Terim | Anlamı |
|------|---------|
| **i18n** | Internationalization (Uluslararasılaştırma) - Uygulamayı çevrilebilir hale getirmek |
| **L10n** | Localization (Yerelleştirme) - Gerçek çevirilerin ve kültürel uyarlamaların yapılması |
| **Locale (Yerel Ayar)**| Dil + Bölge (en-US, tr-TR) |
| **RTL** | Sağdan sola yazılan diller (Arapça, İbranice) |

---

## 2. Ne Zaman i18n Kullanılmalı?

| Proje Türü | i18n Gerekli mi? |
|--------------|--------------|
| Kamuya açık web uygulaması | ✅ Evet |
| SaaS ürünü | ✅ Evet |
| Dahili araç (Internal tool) | ⚠️ Belki |
| Tek bölgeli uygulama | ⚠️ Geleceği planlayın |
| Kişisel proje | ❌ İsteğe bağlı |

---

## 3. Uygulama Desenleri

### React (react-i18next)

```tsx
import { useTranslation } from 'react-i18next';

function Welcome() {
  const { t } = useTranslation();
  return <h1>{t('welcome.title')}</h1>;
}
```

### Next.js (next-intl)

```tsx
import { useTranslations } from 'next-intl';

export default function Page() {
  const t = useTranslations('Home');
  return <h1>{t('title')}</h1>;
}
```

### Python (gettext)

```python
from gettext import gettext as _

print(_("Uygulamamıza hoş geldiniz"))
```

---

## 4. Dosya Yapısı

```
locales/
├── en/
│   ├── common.json
│   ├── auth.json
│   └── errors.json
├── tr/
│   ├── common.json
│   ├── auth.json
│   └── errors.json
└── ar/          # RTL
    └── ...
```

---

## 5. En İyi Pratikler

### YAPIN ✅

- Doğrudan metin yerine çeviri anahtarlarını (translation keys) kullanın.
- Çevirileri özelliklere (feature) göre ad alanlarına (namespace) ayırın.
- Çoğullaştırmayı (pluralization) destekleyin.
- Her yerel ayar (locale) için tarih/sayı formatlarını doğru yönetin.
- Baştan itibaren RTL desteğini planlayın.
- Karmaşık dizeler için ICU mesaj formatını kullanın.

### YAPMAYIN ❌

- Bileşenlerin içinde metinleri hardcode (sabit) yazmayın.
- Çevrilmiş dizeleri manuel olarak birleştirmeyin (concatenate).
- Metin uzunluklarını sabit varsaymayın (Örn: Almanca, İngilizceden %30 daha uzundur).
- RTL düzenini (layout) unutmayın.
- Aynı dosyada dilleri birbirine karıştırmayın.

---

## 6. Yaygın Sorunlar

| Sorun | Çözüm |
|-------|----------|
| Eksik çeviri | Varsayılan dile (fallback) dön |
| Hardcoded metinler | Linter / checker script'i kullan |
| Tarih formatı | `Intl.DateTimeFormat` kullan |
| Sayı formatı | `Intl.NumberFormat` kullan |
| Çoğullaştırma | ICU mesaj formatı kullan |

---

## 7. RTL Desteği (Sağdan Sola)

```css
/* CSS Mantıksal Özellikler (Logical Properties) */
.container {
  margin-inline-start: 1rem;  /* margin-left yerine */
  padding-inline-end: 1rem;   /* padding-right yerine */
}

[dir="rtl"] .icon {
  transform: scaleX(-1);
}
```

---

## 8. Kontrol Listesi

Yayına almadan önce:

- [ ] Kullanıcıya görünen tüm metinler çeviri anahtarlarını kullanıyor.
- [ ] Desteklenen tüm diller için yerel ayar dosyaları mevcut.
- [ ] Tarih/sayı biçimlendirmesi `Intl API` kullanıyor.
- [ ] RTL düzeni test edildi (varsa).
- [ ] Varsayılan (fallback) dil yapılandırıldı.
- [ ] Bileşenlerde hardcoded dize kalmadı.

---

## Script

| Script | Amaç | Komut |
|--------|---------|---------|
| `scripts/i18n_checker.py` | Hardcoded metinleri ve eksik çevirileri tespit et | `python scripts/i18n_checker.py <proje_yolu>` |
