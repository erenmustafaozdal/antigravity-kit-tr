---
name: api-patterns
description: API tasarım prensipleri ve karar verme. REST vs GraphQL vs tRPC seçimi, yanıt formatları, versiyonlama, sayfalama.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# API Desenleri (API Patterns)

> 2025 yılı için API tasarım prensipleri ve karar verme kılavuzu.
> **Sabit desenleri kopyalamayı değil, DÜŞÜNMEYİ öğrenin.**

## 🎯 Seçici Okuma Kuralı

**SADECE istekle ilgili dosyaları okuyun!** İçerik haritasını kontrol edin ve ihtiyacınız olanı bulun.

---

## 📑 İçerik Haritası

| Dosya | Açıklama | Ne Zaman Okunmalı? |
|------|-------------|--------------|
| `api-style.md` | REST vs GraphQL vs tRPC karar ağacı | API türü seçerken |
| `rest.md` | Kaynak isimlendirme, HTTP metodları, durum kodları | REST API tasarlarken |
| `response.md` | Zarf deseni, hata formatı, sayfalama | Yanıt yapısı planlarken |
| `graphql.md` | Şema tasarımı, ne zaman kullanılır, güvenlik | GraphQL değerlendirirken |
| `trpc.md` | TypeScript monorepo, tip güvenliği | TS fullstack projelerinde |
| `versioning.md` | URI/Header/Sorgu versiyonlama | API evrimi planlarken |
| `auth.md` | JWT, OAuth, Passkey, API anahtarları | Auth deseni seçerken |
| `rate-limiting.md` | Token bucket, sliding window | API koruması planlarken |
| `documentation.md` | OpenAPI/Swagger en iyi pratikleri | Dokümantasyon aşamasında |
| `security-testing.md` | OWASP API Top 10, auth/authz testleri | Güvenlik denetimlerinde |

---

## 🔗 İlgili Yetenekler

| İhtiyaç | Yetenek |
|------|-------|
| API uygulaması | `@[skills/backend-development]` |
| Veri yapısı | `@[skills/database-design]` |
| Güvenlik detayları | `@[skills/security-hardening]` |

---

## ✅ Karar Kontrol Listesi

Bir API tasarlamadan önce:

- [ ] **API tüketicileri (istemciler) hakkında kullanıcıya soru soruldu mu?**
- [ ] **BU bağlam için en uygun API stili seçildi mi?** (REST/GraphQL/tRPC)
- [ ] **Tutarlı bir yanıt formatı belirlendi mi?**
- [ ] **Versiyonlama stratejisi planlandı mı?**
- [ ] **Kimlik doğrulama gereksinimleri değerlendirildi mi?**
- [ ] **İstek sınırlama (rate limiting) planlandı mı?**
- [ ] **Dokümantasyon yaklaşımı tanımlandı mı?**

---

## ❌ Anti-Desenler

**YAPMA:**
- Her şey için varsayılan olarak REST kullanma.
- REST uç noktalarında fiiller kullanma (/getUsers gibi).
- Tutarsız yanıt formatları döndürme.
- Dahili hataları (internal errors) istemcilere doğrudan sızdırma.
- İstek sınırlamayı (rate limiting) atlama.

**YAP:**
- API stilini bağlama göre seç.
- İstemci gereksinimlerini sor.
- Kapsamlı dökümante et.
- Uygun HTTP durum kodlarını kullan.

---

## Script

| Script | Amaç | Komut |
|--------|---------|---------|
| `scripts/api_validator.py` | API uç noktası doğrulaması | `python scripts/api_validator.py <project_path>` |
