---
name: web-design-guidelines
description: Web Arayüz Kurallarına uygunluk için UI kodunu incele. "UI'umı incele", "erişilebilirliği kontrol et", "tasarımı denetle", "UX'i incele" veya "sitemi en iyi uygulamalara karşı kontrol et" dendiğinde kullan.
metadata:
  author: vercel
  version: "1.0.0"
  argument-hint: <dosya-veya-desen>
---

# Web Arayüz Kuralları (Web Interface Guidelines)

Dosyaları Web Arayüz Kurallarına uygunluk açısından incele.

## Nasıl Çalışır

1. Aşağıdaki kaynak URL'den en son kuralları al
2. Belirtilen dosyaları oku (veya kullanıcıya dosya/desen sor)
3. Alınan kurallardaki tüm kurallara karşı kontrol et
4. Bulguları özlü `dosya:satır` formatında çıktıla

## Kural Kaynağı

Her incelemeden önce yeni kuralları al:

```
https://raw.githubusercontent.com/vercel-labs/web-interface-guidelines/main/command.md
```

En son kuralları almak için WebFetch kullan. Alınan içerik tüm kuralları ve çıktı formatı talimatlarını içerir.

## Kullanım

Kullanıcı bir dosya veya desen argümanı sağladığında:
1. Yukarıdaki kaynak URL'den kuralları al
2. Belirtilen dosyaları oku
3. Alınan kurallardaki tüm kuralları uygula
4. Kurallarda belirtilen formatı kullanarak bulguları çıktıla

Dosya belirtilmemişse, kullanıcıya hangi dosyaları inceleyeceğini sor.

---

## İlgili Yetenekler

| Yetenek | Ne Zaman Kullanılır |
|---------|---------------------|
| **[frontend-design](../frontend-design/SKILL.md)** | Kodlamadan önce - Tasarım prensiplerini öğren (renk, tipografi, UX psikolojisi) |
| **web-design-guidelines** (bu) | Kodlamadan sonra - Erişilebilirlik, performans ve en iyi uygulamalar için denetle |

## Tasarım İş Akışı

```
1. TASARIM   → frontend-design prensiplerini oku
2. KOD       → Tasarımı uygula
3. DENETLEME → web-design-guidelines incelemesi yap ← BURADASINız
4. DÜZELT    → Denetimden gelen bulguları ele al
```
