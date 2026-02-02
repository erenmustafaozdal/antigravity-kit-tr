---
name: clean-code
description: Pragmatik kodlama standartları - kısa, öz, doğrudan, aşırı mühendislikten ve gereksiz yorumlardan kaçınan yaklaşım
allowed-tools: Read, Write, Edit
version: 2.0
priority: CRITICAL
---

# Temiz Kod - Pragmatik YZ Kodlama Standartları

> **KRİTİK YETENEK** - **Kısa, öz, doğrudan ve çözüm odaklı** olun.

---

## Temel Prensipler

| Prensip | Kural |
|-----------|------|
| **SRP** | Tek Sorumluluk - her fonksiyon/sınıf TEK bir iş yapar |
| **DRY** | Kendini Tekrar Etme - tekrarları çıkar, yeniden kullan |
| **KISS** | Basit Tut - çalışan en basit çözüm |
| **YAGNI** | Buna İhtiyacın Olmayacak - kullanılmayan özellikleri inşa etme |
| **Boy Scout** | İzcilik Kuralı - kodu bulduğundan daha temiz bırak |

---

## İsimlendirme Kuralları

| Öğe | Kural |
|---------|------------|
| **Değişkenler** | Amacı belli etmeli: `n` değil `userCount` |
| **Fonksiyonlar** | Fiil + isim: `user()` değil `getUserById()` |
| **Booleanlar** | Soru formu: `isActive`, `hasPermission`, `canEdit` |
| **Sabitler** | BÜYÜK_HARF_YILAN: `MAX_RETRY_COUNT` |

> **Kural:** Bir ismi açıklamak için yoruma ihtiyaç duyuyorsanız, o ismi değiştirin.

---

## Fonksiyon Kuralları

| Kural | Açıklama |
|------|-------------|
| **Küçük** | Maksimum 20 satır, ideal olan 5-10 satır |
| **Tek İş** | Bir işi yapar ve onu iyi yapar |
| **Tek Seviye** | Fonksiyon başına tek bir soyutlama seviyesi |
| **Az Parametre** | Maksimum 3 argüman, 0-2 tercih edilir |
| **Yan Etki Yok** | Girdileri beklenmedik şekilde değiştirme |

---

## Kod Yapısı

| Desen | Uygulama |
|---------|-------|
| **Guard Clauses** | Uç durumlar için erken dönüşler (early returns) |
| **Düz > İçe İçe** | Derin iç içe yapılardan kaçın (maks 2 seviye) |
| **Kompozisyon** | Küçük fonksiyonların birleşimi |
| **Yakınlık (Colocation)** | İlgili kodu birbirine yakın tut |

---

## YZ Kodlama Tarzı

| Durum | Eylem |
|-----------|--------|
| Kullanıcı özellik ister | Doğrudan yaz |
| Kullanıcı hata bildirir | Çöz, açıklama yapma |
| Gereksinim net değil | Sor, varsayma |

---

## Anti-Desenler (YAPMA!)

| ❌ Desen | ✅ Çözüm |
|-----------|-------|
| Her satırı yorumla | Aşikar yorumları sil |
| Tek satırlık iş için helper | Kodu satır içine (inline) al |
| 2 nesne için Factory yap | Doğrudan örnekle (instantiation) |
| Tek foksiyonlu utils.ts | Kodu kullanıldığı yere koy |
| "Önce import ediyoruz..." | Sadece kodu yaz |
| Derin iç içe yapılar | Guard clause kullan |
| Sihirli sayılar | İsimlendirilmiş sabitler kullan |
| Dev fonksiyonlar | Sorumluluğa göre böl |

---

## 🔴 Herhangi Bir Dosyayı Düzenlemeden ÖNCE (ÖNCE DÜŞÜN!)

**Bir dosyayı değiştirmeden önce kendinize sorun:**

| Soru | Neden |
|----------|-----|
| **Bu dosyayı ne import ediyor?** | Onlar bozulabilir |
| **Bu dosya neyi import ediyor?** | Arayüz değişiklikleri |
| **Bunu hangi testler kapsıyor?** | Testler başarısız olabilir |
| **Bu paylaşılan bir bileşen mi?** | Birden fazla yer etkilenebilir |

**Hızlı Kontrol:**
```
Düzenlenecek Dosya: UserService.ts
└── Bunu kim import ediyor? → UserController.ts, AuthController.ts
└── Onların da değişikliğe ihtiyacı var mı? → Fonksiyon imzalarını kontrol et
```

> 🔴 **Kural:** Dosyayı ve tüm bağımlı dosyaları AYNI görevde düzenleyin.
> 🔴 **Asla bozuk importlar veya eksik güncellemeler bırakmayın.**

---

## Özet

| Yap | Yapma |
|----|-------|
| Kodu doğrudan yaz | Eğitim (tutorial) verme |
| Kodun kendini belgelemesini sağla | Aşikar yorumlar ekleme |
| Hataları hemen düzelt | Önce düzeltmeyi açıklama |
| Küçük şeyleri satır içine al | Gereksiz dosyalar oluşturma |
| İsimleri net seç | Kısaltmalar kullanma |
| Fonksiyonları küçük tut | 100+ satırlık fonksiyonlar yazma |

> **Unutma: Kullanıcı programlama dersi değil, çalışan kod istiyor.**

---

## 🔴 Tamamlamadan Önce Öz-Kontrol (ZORUNLU)

**"Görev tamamlandı" demeden önce doğrulayın:**

| Kontrol | Soru |
|-------|----------|
| ✅ **Hedef karşılandı mı?** | Tam olarak kullanıcının istediğini yaptım mı? |
| ✅ **Dosyalar düzenlendi mi?** | Gerekli tüm dosyaları değiştirdim mi? |
| ✅ **Kod çalışıyor mu?** | Değişikliği test ettim mi/doğruladım mı? |
| ✅ **Hata yok mu?** | Lint ve TypeScript geçiyor mu? |
| ✅ **Unutulan bir şey var mı?** | Atlanan bir uç durum (edge case) var mı? |

> 🔴 **Kural:** Herhangi bir kontrol başarısız olursa, tamamlamadan önce düzeltin.

---

## Doğrulama Scriptleri (ZORUNLU)

> 🔴 **KRİTİK:** Her ajan, işini tamamladıktan sonra SADECE kendi yeteneğine ait scriptleri çalıştırır.

### Ajan → Script Eşleşmesi

| Ajan | Script | Komut |
|-------|--------|---------|
| **frontend-specialist** | UX Denetimi | `python .agent/skills/frontend-design/scripts/ux_audit.py .` |
| **frontend-specialist** | Erişilebilirlik | `python .agent/skills/frontend-design/scripts/accessibility_checker.py .` |
| **backend-specialist** | API Doğrulayıcı | `python .agent/skills/api-patterns/scripts/api_validator.py .` |
| **mobile-developer** | Mobil Denetim | `python .agent/skills/mobile-design/scripts/mobile_audit.py .` |
| **database-architect** | Şema Doğrulama | `python .agent/skills/database-design/scripts/schema_validator.py .` |
| **security-auditor** | Güvenlik Tarama | `python .agent/skills/vulnerability-scanner/scripts/security_scan.py .` |
| **seo-specialist** | SEO Kontrolü | `python .agent/skills/seo-fundamentals/scripts/seo_checker.py .` |
| **seo-specialist** | GEO Kontrolü | `python .agent/skills/geo-fundamentals/scripts/geo_checker.py .` |
| **performance-optimizer** | Lighthouse | `python .agent/skills/performance-profiling/scripts/lighthouse_audit.py <url>` |
| **test-engineer** | Test Çalıştırıcı | `python .agent/skills/testing-patterns/scripts/test_runner.py .` |
| **test-engineer** | Playwright | `python .agent/skills/webapp-testing/scripts/playwright_runner.py <url>` |
| **Herhangi bir ajan** | Lint Kontrolü | `python .agent/skills/lint-and-validate/scripts/lint_runner.py .` |
| **Herhangi bir ajan** | Tip Kapsamı | `python .agent/skills/lint-and-validate/scripts/type_coverage.py .` |
| **Herhangi bir ajan** | i18n Kontrolü | `python .agent/skills/i18n-localization/scripts/i18n_checker.py .` |

> ❌ **YANLIŞ:** `test-engineer` ajanının `ux_audit.py` çalıştırması
> ✅ **DOĞRU:** `frontend-specialist` ajanının `ux_audit.py` çalıştırması

---

### 🔴 Script Çıktısı Yönetimi (OKU → ÖZETLE → SOR)

**Bir doğrulama scripti çalıştırırken ŞUNLARI YAPMALISINIZ:**

1. **Scripti çalıştırın** ve TÜM çıktıyı yakalayın
2. **Çıktıyı ayrıştırın** - hataları, uyarıları ve geçenleri belirleyin
3. **Kullanıcıya bu formatta özetleyin:**

```markdown
## Script Sonuçları: [script_adi.py]

### ❌ Bulunan Hatalar (X adet)
- [Dosya:Satır] Hata açıklaması 1
- [Dosya:Satır] Hata açıklaması 2

### ⚠️ Uyarılar (Y adet)
- [Dosya:Satır] Uyarı açıklaması

### ✅ Geçenler (Z adet)
- Kontrol 1 geçti
- Kontrol 2 geçti

**X adet hatayı düzelteyim mi?**
```

4. **Düzeltmeden önce** kullanıcı onayını bekleyin
5. **Düzelttikten sonra** → Onaylamak için scripti tekrar çalıştırın

> 🔴 **İHLAL:** Scripti çalıştırıp çıktıyı görmezden gelmek = BAŞARISIZ görev.
> 🔴 **İHLAL:** Sormadan otomatik düzeltme yapmak = İzin verilmez.
> 🔴 **Kural:** Her zaman ÖNCE OKU → ÖZETLE → SOR → sonra düzelt.
