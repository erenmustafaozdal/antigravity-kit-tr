---
name: database-design
description: Veritabanı tasarım prensipleri ve karar verme. Şema tasarımı, indeksleme stratejisi, ORM seçimi, sunucusuz (serverless) veritabanları.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# Veritabanı Tasarımı (Database Design)

> **Sadece SQL kalıplarını kopyalamayı değil, DÜŞÜNMEYİ öğrenin.**

## 🎯 Seçici Okuma Kuralı

**SADECE istekle ilgili dosyaları okuyun!** İçerik haritasını kontrol edin ve ihtiyacınız olanı bulun.

| Dosya | Açıklama | Ne Zaman Okunmalı? |
|------|-------------|--------------|
| `database-selection.md` | PostgreSQL vs Neon vs Turso vs SQLite | Veritabanı seçerken |
| `orm-selection.md` | Drizzle vs Prisma vs Kysely | ORM seçerken |
| `schema-design.md` | Normalizasyon, PK'ler, ilişkiler | Şema tasarlarken |
| `indexing.md` | İndeks türleri, bileşik indeksler | Performans iyileştirirken |
| `optimization.md` | N+1 problemi, EXPLAIN ANALYZE | Sorgu optimizasyonu yaparken |
| `migrations.md` | Güvenli migrasyonlar, sunucusuz veritabanları | Şema değişikliklerinde |

---

## ⚠️ Temel Prensip

- Belirsiz durumlarda veritabanı tercihlerini kullanıcıya SORUN.
- Veritabanı/ORM seçimini BAĞLAM'a (context) göre yapın.
- Her şey için varsayılan olarak PostgreSQL'i seçmeyin.

---

## Karar Kontrol Listesi

Şema tasarlamadan önce:

- [ ] Veritabanı tercihi hakkında kullanıcıya soruldu mu?
- [ ] BU bağlam için uygun veritabanı seçildi mi?
- [ ] Dağıtım (deployment) ortamı değerlendirildi mi?
- [ ] İndeks stratejisi planlandı mı?
- [ ] İlişki türleri tanımlandı mı?

---

## Anti-Desenler

❌ Basit uygulamalar için varsayılan olarak PostgreSQL seçmek (SQLite yeterli olabilir)
❌ İndekslemeyi atlamak
❌ Prodüksiyonda SELECT * kullanmak
❌ Yapılandırılmış verinin daha iyi olduğu durumlarda JSON saklamak
❌ N+1 sorgu problemlerini görmezden gelmek
