---
name: tdd-workflow
description: Test-Driven Development iş akışı prensipleri. RED-GREEN-REFACTOR döngüsü.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# TDD İş Akışı (TDD Workflow)

> Önce testleri yaz, sonra kodu.

---

## 1. TDD Döngüsü

```
🔴 RED → Başarısız test yaz
    ↓
🟢 GREEN → Geçmesi için minimal kod yaz
    ↓
🔵 REFACTOR → Kod kalitesini iyileştir
    ↓
   Tekrarla...
```

---

## 2. TDD'nin Üç Yasası

1. Yalnızca başarısız bir testi geçirmek için üretim kodu yaz
2. Başarısızlığı göstermek için yalnızca yeterli test yaz
3. Testi geçirmek için yalnızca yeterli kod yaz

---

## 3. RED Aşaması Prensipleri

### Ne Yazılır

| Odak | Örnek |
|------|-------|
| Davranış | "İki sayıyı toplamalı" |
| Uç durumlar | "Boş girdiyi işlemeli" |
| Hata durumları | "Geçersiz veri için fırlatmalı" |

### RED Aşaması Kuralları

- Test önce başarısız olmalı
- Test adı beklenen davranışı tanımlar
- Test başına bir assertion (ideal olarak)

---

## 4. GREEN Aşaması Prensipleri

### Minimum Kod

| Prensip | Anlamı |
|---------|--------|
| **YAGNI** | İhtiyaç Duymayacaksın |
| **En basit şey** | Geçmek için minimumu yaz |
| **Optimizasyon yok** | Sadece çalışmasını sağla |

### GREEN Aşaması Kuralları

- Gereksiz kod yazma
- Henüz optimize etme
- Testi geç, başka bir şey yapma

---

## 5. REFACTOR Aşaması Prensipleri

### Neleri İyileştirmelim

| Alan | Eylem |
|------|-------|
| Tekrarlama | Ortak kodu çıkar |
| İsimlendirme | Niyeti açık hale getir |
| Yapı | Organizasyonu iyileştir |
| Karmaşıklık | Mantığı basitleştir |

### REFACTOR Kuralları

- Tüm testler yeşil kalmalı
- Küçük artımlı değişiklikler
- Her refactor'dan sonra commit yap

---

## 6. AAA Deseni

Her test şunu takip eder:

| Adım | Amaç |
|------|------|
| **Arrange** | Test verisini hazırla |
| **Act** | Test edilen kodu çalıştır |
| **Assert** | Beklenen sonucu doğrula |

---

## 7. TDD Ne Zaman Kullanılır

| Senaryo | TDD Değeri |
|---------|-----------|
| Yeni özellik | Yüksek |
| Hata düzeltme | Yüksek (önce test yaz) |
| Karmaşık mantık | Yüksek |
| Keşifsel | Düşük (spike, sonra TDD) |
| UI yerleşimi | Düşük |

---

## 8. Test Önceliklendirme

| Öncelik | Test Tipi |
|---------|-----------|
| 1 | Mutlu yol |
| 2 | Hata durumları |
| 3 | Uç durumlar |
| 4 | Performans |

---

## 9. Anti-Desenler

| ❌ Yapma | ✅ Yap |
|----------|--------|
| RED aşamasını atla | Önce testin başarısız olmasını izle |
| Testleri sonra yaz | Testleri önce yaz |
| İlk aşamada aşırı mühendislik yap | Basit tut |
| Birden fazla assertion | Davranış başına bir test |
| Implementasyonu test et | Davranışı test et |

---

## 10. AI ile Güçlendirilmiş TDD

### Çoklu-Agent Deseni

| Agent | Rol |
|-------|-----|
| Agent A | Başarısız testler yaz (RED) |
| Agent B | Geçmesi için uygula (GREEN) |
| Agent C | Optimize et (REFACTOR) |

---

> **Unutma:** Test, spesifikasyondur. Bir test yazamıyorsan, gereksinimi anlamıyorsun.
