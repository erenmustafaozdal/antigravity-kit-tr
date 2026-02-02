---
name: code-review-checklist
description: Kod kalitesi, güvenlik ve en iyi pratikleri kapsayan kod inceleme yönergeleri.
allowed-tools: Read, Glob, Grep
---

# Kod İnceleme Kontrol Listesi (Code Review Checklist)

## Hızlı İnceleme Listesi

### Doğruluk (Correctness)
- [ ] Kod yapması gereken işi yapıyor mu?
- [ ] Uç durumlar (edge cases) yönetildi mi?
- [ ] Hata yönetimi (error handling) yerinde mi?
- [ ] Belirgin bir hata (bug) var mı?

### Güvenlik (Security)
- [ ] Girdiler doğrulandı ve temizlendi mi (validation & sanitization)?
- [ ] SQL/NoSQL enjeksiyon açıklarına karşı önlem alındı mı?
- [ ] XSS veya CSRF açıkları var mı?
- [ ] Kod içinde hardcoded gizli bilgiler veya hassas veriler var mı?
- [ ] **YZ'ye Özel:** Prompt Injection saldırılarına karşı koruma var mı (varsa)?
- [ ] **YZ'ye Özel:** YZ çıktıları kritik işlemlerde kullanılmadan önce temizleniyor mu?

### Performans
- [ ] N+1 sorgu problemi var mı?
- [ ] Gereksiz döngülerden kaçınıldı mı?
- [ ] Uygun önbellekleme (caching) yapıldı mı?
- [ ] Paket boyutu (bundle size) üzerindeki etkisi değerlendirildi mi?

### Kod Kalitesi
- [ ] İsimlendirmeler net mi?
- [ ] DRY - kendini tekrar eden kod var mı?
- [ ] SOLID prensiplerine uyulmuş mu?
- [ ] Soyutlama seviyesi uygun mu?

### Test Etme
- [ ] Yeni kod için unit testler yazıldı mı?
- [ ] Uç durumlar test edildi mi?
- [ ] Testler okunabilir ve sürdürülebilir mi?

### Dokümantasyon
- [ ] Karmaşık mantık içeren kısımlar yorumlandı mı?
- [ ] Genel (public) API'ler dökümante edildi mi?
- [ ] Gerekiyorsa README güncellendi mi?

## YZ ve LLM İnceleme Desenleri (2025)

### Mantık ve Halüsinasyonlar
- [ ] **Düşünce Zinciri (Chain of Thought):** Mantık doğrulanabilir bir yolu takip ediyor mu?
- [ ] **Uç Durumlar:** YZ boş durumları, zaman aşımlarını ve kısmi hataları hesaba kattı mı?
- [ ] **Harici Durum:** Kod, dosya sistemleri veya ağlar hakkında güvenli varsayımlarda bulunuyor mu?

### Prompt Mühendisliği İncelemesi
```markdown
// ❌ Kodda belirsiz prompt kullanımı
const response = await ai.generate(userInput);

// ✅ Yapılandırılmış ve güvenli prompt kullanımı
const response = await ai.generate({
  system: "Özel bir çözümleyici (parser) rolündesiniz...",
  input: sanitize(userInput),
  schema: ResponseSchema
});
```

## İşaretlenmesi Gereken Anti-Desenler

```typescript
// ❌ Sihirli sayılar (Magic numbers)
if (status === 3) { ... }

// ✅ İsimlendirilmiş sabitler
if (status === Status.ACTIVE) { ... }

// ❌ Derin iç içe yapılar
if (a) { if (b) { if (c) { ... } } }

// ✅ Erken dönüşler (Early returns)
if (!a) return;
if (!b) return;
if (!c) return;
// asıl işi yap

// ❌ Uzun fonksiyonlar (100+ satır)
// ✅ Küçük, odaklanmış fonksiyonlar

// ❌ any tipi kullanımı
const data: any = ...

// ✅ Uygun tiplerin kullanımı
const data: UserData = ...
```

## İnceleme Yorumları Rehberi

```
// Engelleyici (blocking) sorunlar için 🔴 kullanın
🔴 ENGELLEYİCİ: Burada SQL injection açığı var.

// Önemli öneriler için 🟡 kullanın
🟡 ÖNERİ: Performans için useMemo kullanmayı değerlendirin.

// Küçük düzeltmeler (nit) için 🟢 kullanın
🟢 NOT: Değişmez değişkenler için let yerine const tercih edin.

// Sorular için ❓ kullanın
❓ SORU: Burada kullanıcı null gelirse ne olur?
```
