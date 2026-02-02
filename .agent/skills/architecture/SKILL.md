---
name: architecture
description: Mimari karar verme çerçevesi. Gereksinim analizi, takas (trade-off) değerlendirmesi, ADR dokümantasyonu. Mimari kararlar alırken veya sistem tasarımını analiz ederken kullanın.
allowed-tools: Read, Glob, Grep
---

# Mimari Karar Çerçevesi (Architecture Decision Framework)

> "Gereksinimler mimariyi yönlendirir. Takaslar kararları şekillendirir. ADR'ler gerekçeleri kaydeder."

## 🎯 Seçici Okuma Kuralı

**SADECE istekle ilgili dosyaları okuyun!** İçerik haritasını kontrol edin ve ihtiyacınız olanı bulun.

| Dosya | Açıklama | Ne Zaman Okunmalı? |
|------|-------------|--------------|
| `context-discovery.md` | Sorulacak sorular, proje sınıflandırması | Mimari tasarıma başlarken |
| `trade-off-analysis.md` | ADR şablonları, takas çerçevesi | Kararları dökümante ederken |
| `pattern-selection.md` | Karar ağaçları, anti-desenler | Desen seçerken |
| `examples.md` | MVP, SaaS, Kurumsal örnekler | Referans uygulamalar için |
| `patterns-reference.md` | Desenler için hızlı bakış | Desen karşılaştırması için |

---

## 🔗 İlgili Yetenekler

| Yetenek | Kullanım Amacı |
|-------|---------|
| `@[skills/database-design]` | Veritabanı şema tasarımı |
| `@[skills/api-patterns]` | API tasarım desenleri |
| `@[skills/deployment-procedures]` | Dağıtım mimarisi |

---

## Temel Prensip

**"Basitlik en yüksek gelişmişlik düzeyidir."**

- Basit başlayın.
- Karmaşıklığı SADECE gerekli olduğu kanıtlandığında ekleyin.
- Desenleri daha sonra her zaman ekleyebilirsiniz.
- Karmaşıklığı kaldırmak, eklemekten ÇOK daha zordur.

---

## Doğrulama Kontrol Listesi

Mimariyi kesinleştirmeden önce:

- [ ] Gereksinimler net bir şekilde anlaşıldı mı?
- [ ] Kısıtlamalar belirlendi mi?
- [ ] Her kararın takas (trade-off) analizi yapıldı mı?
- [ ] Daha basit alternatifler değerlendirildi mi?
- [ ] Önemli kararlar için ADR'ler yazıldı mı?
- [ ] Ekibin uzmanlığı seçilen desenlerle örtüşüyor mu?
