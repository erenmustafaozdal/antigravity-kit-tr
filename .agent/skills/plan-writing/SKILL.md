---
name: plan-writing
description: Açık kırılımlar, bağımlılıklar ve doğrulama kriterleri ile yapılandırılmış görev planlama. Özellik uygularken, refactoring yaparken veya herhangi bir çok adımlı işte kullan.
allowed-tools: Read, Glob, Grep
---

# Plan Yazma (Plan Writing)

> Kaynak: obra/superpowers

## Genel Bakış
Bu yetenek, işi doğrulama kriterleri ile açık, eylem yapılabilir görevlere ayırmak için bir framework sağlar.

## Görev Kırılım Prensipleri

### 1. Küçük, Odaklanmış Görevler
- Her görev 2-5 dakika sürmeli
- Görev başına bir açık sonuç
- Bağımsız olarak doğrulanabilir

### 2. Açık Doğrulama
- Bittiğini nasıl bilirsin?
- Neyi kontrol edebilir/test edebilirsin?
- Beklenen çıktı nedir?

### 3. Mantıksal Sıralama
- Bağımlılıklar tanımlandı
- Mümkün olduğunda paralel iş
- Kritik yol vurgulandı
- **Faz X: Doğrulama her zaman SON**

### 4. Proje Root'unda Dinamik İsimlendirme
- Plan dosyaları PROJE ROOT'unda `{task-slug}.md` olarak kaydedilir
- İsim görevden türetilir (örn. "auth ekle" → `auth-feature.md`)
- **ASLA** `.claude/`, `docs/` veya geçici klasörlerde değil

## Planlama Prensipleri (Şablon DEĞİL!)

> 🔴 **Sabit şablon YOK. Her plan göreve ÖZGÜ.**

### Prensip 1: KISA Tut

| ❌ Yanlış | ✅ Doğru |
|-----------|----------|
| Alt-alt görevler ile 50 görev | Maks 5-10 açık görev |
| Her mikro adım listelendi | Yalnızca eylem yapılabilir öğeler |
| Ayrıntılı açıklamalar | Görev başına bir satır |

> **Kural:** Plan 1 sayfadan uzunsa, çok uzun. Basitleştir.

---

### Prensip 2: SPESİFİK ol, Genel Değil

| ❌ Yanlış | ✅ Doğru |
|-----------|----------|
| "Projeyi kur" | "`npx create-next-app` çalıştır" |
| "Kimlik doğrulama ekle" | "next-auth kur, `/api/auth/[...nextauth].ts` oluştur" |
| "UI'ı stillendir" | "`Header.tsx`'e Tailwind sınıfları ekle" |

> **Kural:** Her görevin açık, doğrulanabilir bir sonucu olmalı.

---

### Prensip 3: Proje Tipine Göre Dinamik İçerik

**YENİ PROJE İÇİN:**
- Hangi teknoloji yığını? (önce karar ver)
- MVP nedir? (minimal özellikler)
- Dosya yapısı nedir?

**ÖZELLİK EKLEMEK İÇİN:**
- Hangi dosyalar etkilenir?
- Hangi bağımlılıklar gerekli?
- Nasıl çalıştığı doğrulanır?

**HATA DÜZELTİMİ İÇİN:**
- Kök neden nedir?
- Hangi dosya/satır değiştirilmeli?
- Düzeltme nasıl test edilir?

---

### Prensip 4: Script'ler Projeye Özgüdür

> 🔴 **Script komutlarını kopyala-yapıştır YAPMA. Proje tipine göre seç.**

| Proje Tipi | İlgili Script'ler |
|------------|-------------------|
| Frontend/React | `ux_audit.py`, `accessibility_checker.py` |
| Backend/API | `api_validator.py`, `security_scan.py` |
| Mobil | `mobile_audit.py` |
| Veritabanı | `schema_validator.py` |
| Full-stack | Dokunduğun şeye göre yukarıdakilerin karışımı |

**Yanlış:** Her plana tüm script'leri eklemek
**Doğru:** Yalnızca BU göreve ilgili script'ler

---

### Prensip 5: Doğrulama Basittir

| ❌ Yanlış | ✅ Doğru |
|-----------|----------|
| "Componentin doğru çalıştığını doğrula" | "`npm run dev` çalıştır, butona tıkla, toast gör" |
| "API'yi test et" | "curl localhost:3000/api/users 200 döndürür" |
| "Stilleri kontrol et" | "Tarayıcıyı aç, dark mode açma-kapama işlevini doğrula" |

---

## Plan Yapısı (Esnek, Sabit Değil!)

```
# [Görev Adı]

## Hedef
Tek cümle: Ne inşa ediyoruz/düzeltiyoruz?

## Görevler
- [ ] Görev 1: [Spesifik eylem] → Doğrula: [Nasıl kontrol edilir]
- [ ] Görev 2: [Spesifik eylem] → Doğrula: [Nasıl kontrol edilir]
- [ ] Görev 3: [Spesifik eylem] → Doğrula: [Nasıl kontrol edilir]

## Bittiğinde
- [ ] [Ana başarı kriteri]
```

> **Bu kadar.** Gerçekten gerekmedikçe faz yok, alt bölüm yok.
> Minimal tut. Karmaşıklığı yalnızca gerektiğinde ekle.

## Notlar
[Önemli değerlendirmeler]
```

---

## En İyi Uygulamalar (Hızlı Referans)

1. **Hedefle başla** - Ne inşa ediyoruz/düzeltiyoruz?
2. **Maks 10 görev** - Daha fazlaysa, birden fazla plana böl
3. **Her görev doğrulanabilir** - Açık "bitti" kriteri
4. **Projeye özgü** - Şablon kopyala-yapıştır yok
5. **Giderken güncelle** - Tamamlandığında `[x]` işaretle

---

## Ne Zaman Kullanılır

- Sıfırdan yeni proje
- Özellik ekleme
- Hata düzeltme (karmaşıksa)
- Birden fazla dosyayı refactoring
