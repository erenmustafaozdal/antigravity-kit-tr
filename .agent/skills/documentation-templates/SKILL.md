---
name: documentation-templates
description: Dokümantasyon şablonları ve yapı kuralları. README, API dökümanları, kod yorumları ve YZ dostu dokümantasyon.
allowed-tools: Read, Glob, Grep
---

# Dokümantasyon Şablonları

> Yaygın dokümantasyon türleri için şablonlar ve yapı kuralları.

---

## 1. README Yapısı

### Temel Bölümler (Öncelik Sırasına Göre)

| Bölüm | Amaç |
|---------|---------|
| **Başlık + Tek Cümlelik Özet** | Bu nedir? |
| **Hızlı Başlangıç** | <5 dakikada çalıştırma |
| **Özellikler** | Neler yapabilirim? |
| **Yapılandırma (Configuration)** | Özelleştirme nasıl yapılır? |
| **API Referansı** | Detaylı döküman linki |
| **Katkıda Bulunma** | Nasıl yardımcı olabilirim? |
| **Lisans** | Yasal durum |

### README Şablonu

```markdown
# Proje Adı

Tek cümlelik kısa açıklama.

## Hızlı Başlangıç

[Çalıştırmak için minimum adımlar]

## Özellikler

- Özellik 1
- Özellik 2

## Yapılandırma

| Değişken | Açıklama | Varsayılan |
|----------|-------------|---------|
| PORT | Sunucu portu | 3000 |

## Dokümantasyon

- [API Referansı](./docs/api.md)
- [Mimari](./docs/architecture.md)

## Lisans

MIT
```

---

## 2. API Dokümantasyon Yapısı

### Uç Nokta (Endpoint) Başına Şablon

```markdown
## GET /users/:id

ID'ye göre kullanıcıyı getirir.

**Parametreler:**
| Ad | Tür | Zorunlu | Açıklama |
|------|------|----------|-------------|
| id | string | Evet | Kullanıcı ID'si |

**Yanıt:**
- 200: Kullanıcı nesnesi
- 404: Kullanıcı bulunamadı

**Örnek:**
[İstek ve yanıt örneği]
```

---

## 3. Kod Yorumlama Kuralları

### JSDoc/TSDoc Şablonu

```typescript
/**
 * Fonksiyonun ne yaptığının kısa açıklaması.
 * 
 * @param paramName - Parametrenin açıklaması
 * @returns Dönüş değerinin açıklaması
 * @throws ErrorType - Bu hata ne zaman oluşur?
 * 
 * @example
 * const result = fonksiyonAdi(input);
 */
```

### Ne Zaman Yorum Eklenmeli?

| ✅ Yorumla | ❌ Yorumlama |
|-----------|-----------------|
| Neden (iş mantığı) | Ne (aşikar olan) |
| Karmaşık algoritmalar | Her satırı |
| Aşikar olmayan davranışlar | Kendi kendini açıklayan kod |
| API sözleşmeleri | Uygulama detayları |

---

## 4. Değişim Günlüğü (Changelog) Şablonu

```markdown
# Değişim Günlüğü (Changelog)

## [Yayınlanmamış]
### Eklendi
- Yeni özellik

## [1.0.0] - 2025-01-01
### Eklendi
- İlk sürüm
### Değişti
- Bağımlılıklar güncellendi
### Düzeltildi
- Hata düzeltmesi
```

---

## 5. Mimari Karar Kaydı (ADR)

```markdown
# ADR-001: [Başlık]

## Durum
Kabul Edildi / Kullanımdan Kaldırıldı / Yerine Başkası Geldi

## Bağlam (Context)
Bu kararı neden alıyoruz?

## Karar
Neye karar verdik?

## Sonuçlar
Takaslar (trade-offs) nelerdir?
```

---

## 6. YZ Dostu Dokümantasyon (2025)

### llms.txt Şablonu

YZ tarayıcıları ve ajanları için:

```markdown
# Proje Adı
> Tek cümlelik hedef.

## Temel Dosyalar
- [src/index.ts]: Ana giriş noktası
- [src/api/]: API rotaları
- [docs/]: Dokümantasyon

## Temel Kavramlar
- Kavram 1: Kısa açıklama
- Kavram 2: Kısa açıklama
```

### MCP-Uyumlu Dokümantasyon

RAG indeksi için:
- Net H1-H3 hiyerarşisi
- Veri yapıları için JSON/YAML örnekleri
- Akışlar için Mermaid diyagramları
- Kendi kendine yeten (self-contained) bölümler

---

## 7. Yapı Prensipleri

| Prensip | Neden? |
|-----------|-----|
| **Taranabilir** | Başlıklar, listeler, tablolar |
| **Önce Örnekler** | Sadece anlatma, göster |
| **Kademeli Detaylandırma** | Basit → Karmaşık |
| **Güncel** | Güncel olmayan döküman yanıltıcıdır |

---

> **Unutmayın:** Şablonlar başlangıç noktalarıdır. Projenizin ihtiyaçlarına göre uyarlayın.
