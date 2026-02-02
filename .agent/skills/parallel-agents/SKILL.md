---
name: parallel-agents
description: Çoklu-agent orkestrasyon desenleri. Bağımsız görevler farklı alan uzmanlığı ile çalışabildiğinde veya kapsamlı analiz birden fazla perspektif gerektirdiğinde kullan.
allowed-tools: Read, Glob, Grep
---

# Native Paralel Agentler

> Antigravity'nin yerleşik Agent Aracı ile orkestrasyon

## Genel Bakış

Bu yetenek, Antigravity'nin yerel agent sistemi aracılığıyla birden fazla özelleşmiş agent'ı koordine etmeyi sağlar. Harici script'lerin aksine, bu yaklaşım tüm orkestrasyonu Antigravity'nin kontrolü altında tutar.

## Orkestrasyonu Ne Zaman Kullanmalı

✅ **İyi:**
- Birden fazla uzmanlık alanı gerektiren karmaşık görevler
- Güvenlik, performans ve kalite perspektiflerinden kod analizi
- Kapsamlı incelemeler (mimari + güvenlik + test)
- Backend + frontend + veritabanı işi gerektiren özellik implementasyonu

❌ **Uygun değil:**
- Basit, tek alanlı görevler
- Hız lı düzeltmeler veya küçük değişiklikler
- Bir agent'ın yeterli olduğu görevler

---

## Native Agent Çağırma

### Tek Agent
```
Kimlik doğrulama incelemesi için security-auditor agent'ını kullan
```

### Sıralı Zincir
```
Önce, proje yapısını keşfetmek için explorer-agent'ı kullan.
Sonra, API uç noktalarını incelemek için backend-specialist kullan.
Son olarak, test açıklarını tanımlamak için test-engineer kullan.
```

### Bağlam Aktarma ile
```
React componentlerini analiz etmek için frontend-specialist kullan.
Bu bulgulara dayanarak, test-engineer'ın component testleri oluşturmasını sağla.
```

### Önceki İşi Devam Ettir
```
Agent [agentId]'yi devam ettir ve ek gereksinimlerle devam et.
```

---

## Orkestrasyon Desenleri

### Desen 1: Kapsamlı Analiz
```
Agentler: explorer-agent → [domain-agents] → sentez

1. explorer-agent: Kod tabanı yapısını haritalama
2. security-auditor: Güvenlik duruşu
3. backend-specialist: API kalitesi
4. frontend-specialist: UI/UX desenleri
5. test-engineer: Test kapsamı
6. Tüm bulguları sentezle
```

### Desen 2: Özellik İncelemesi
```
Agentler: etkilenen-domain-agentleri → test-engineer

1. Etkilenen alanları tanımla (backend? frontend? ikisi?)
2. İlgili domain agentlerini çağır
3. test-engineer değişiklikleri doğrular
4. Önerileri sentezle
```

### Desen 3: Güvenlik Denetimi
```
Agentler: security-auditor → penetration-tester → sentez

1. security-auditor: Yapılandırma ve kod incelemesi
2. penetration-tester: Aktif güvenlik açığı testi
3. Önceliklendirilmiş düzeltme ile sentezle
```

---

## Mevcut Agentler

| Agent | Uzmanlık | Tetikleyici İfadeler |
|-------|----------|----------------------|
| `orchestrator` | Koordinasyon | "kapsamlı", "çoklu-perspektif" |
| `security-auditor` | Güvenlik | "güvenlik", "auth", "güvenlik açıkları" |
| `penetration-tester` | Güvenlik Testi | "pentest", "red team", "exploit" |
| `backend-specialist` | Backend | "API", "sunucu", "Node.js", "Express" |
| `frontend-specialist` | Frontend | "React", "UI", "componentler", "Next.js" |
| `test-engineer` | Test Etme | "testler", "kapsam", "TDD" |
| `devops-engineer` | DevOps | "deploy", "CI/CD", "altyapı" |
| `database-architect` | Veritabanı | "şema", "Prisma", "migrasyonlar" |
| `mobile-developer` | Mobil | "React Native", "Flutter", "mobil" |
| `api-designer` | API Tasarımı | "REST", "GraphQL", "OpenAPI" |
| `debugger` | Hata Ayıklama | "hata", "bug", "çalışmıyor" |
| `explorer-agent` | Keşif | "keşfet", "haritalama", "yapı" |
| `documentation-writer` | Dokümantasyon | "doküman yaz", "README oluştur", "API dokümanı üret" |
| `performance-optimizer` | Performans | "yavaş", "optimize et", "profilleme" |
| `project-planner` | Planlama | "plan", "yol haritası", "kilometre taşları" |
| `seo-specialist` | SEO | "SEO", "meta etiketleri", "arama sıralaması" |
| `game-developer` | Oyun Geliştirme | "oyun", "Unity", "Godot", "Phaser" |

---

## Antigravity Yerleşik Agentleri

Bunlar özel agentlerle birlikte çalışır:

| Agent | Model | Amaç |
|-------|-------|------|
| **Explore** | Haiku | Hızlı salt-okunur kod tabanı arama |
| **Plan** | Sonnet | Plan modunda araştırma |
| **General-purpose** | Sonnet | Karmaşık çok adımlı değişiklikler |

Hızlı aramalar için **Explore**, alan uzmanlığı için **özel agentler** kullan.

---

## Sentez Protokolü

Tüm agentler tamamlandıktan sonra, sentezle:

```markdown
## Orkestrasyon Sentezi

### Görev Özeti
[Başarılan şeyler]

### Agent Katkıları
| Agent | Bulgu |
|-------|-------|
| security-auditor | X bulundu |
| backend-specialist | Y tanımlandı |

### Konsolide Öneriler
1. **Kritik**: [Agent A'dan Sorun]
2. **Önemli**: [Agent B'den Sorun]
3. **İyi olur**: [Agent C'den İyileştirme]

### Eylem Öğeleri
- [ ] Kritik güvenlik sorununu düzelt
- [ ] API uç noktasını refactor et
- [ ] Eksik testleri ekle
```

---

## En İyi Uygulamalar

1. **Mevcut agentler** - 17 özelleşmiş agent orkestre edilebilir
2. **Mantıksal sıra** - Keşif → Analiz → İmplementasyon → Test
3. **Bağlam paylaş** - İlgili bulguları sonraki agentlere aktar
4. **Tek sentez** - Ayrı çıktılar değil, birleşik bir rapor
5. **Değişiklikleri doğrula** - Kod değişiklikleri için her zaman test-engineer dahil et

---

## Ana Faydalar

- ✅ **Tek oturum** - Tüm agentler bağlamı paylaşır
- ✅ **AI-kontrollü** - Claude özerk olarak orkestre eder
- ✅ **Yerel entegrasyon** - Yerleşik Explore, Plan agentleri ile çalışır
- ✅ **Devam ettirme desteği** - Önceki agent işine devam edebilir
- ✅ **Bağlam aktarma** - Bulgular agentler arasında akar
