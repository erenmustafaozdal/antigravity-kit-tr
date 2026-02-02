---
name: mcp-builder
description: MCP (Model Context Protocol) sunucu oluşturma prensipleri. Araç tasarımı, kaynak desenleri, en iyi uygulamalar.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# MCP Oluşturucu (MCP Builder)

> MCP sunucuları oluşturmak için prensipler.

---

## 1. MCP Genel Bakış

### MCP Nedir?

Model Context Protocol - AI sistemlerini harici araçlar ve veri kaynaklarıyla bağlamak için standart.

### Temel Kavramlar

| Kavram | Amaç |
|--------|------|
| **Tools** | AI'ın çağırabileceği fonksiyonlar |
| **Resources** | AI'ın okuyabileceği veriler |
| **Prompts** | Önceden tanımlanmış prompt şablonları |

---

## 2. Sunucu Mimarisi

### Proje Yapısı

```
my-mcp-server/
├── src/
│   └── index.ts      # Ana giriş
├── package.json
└── tsconfig.json
```

### Transport Tipleri

| Tip | Kullanım |
|-----|----------|
| **Stdio** | Yerel, CLI-tabanlı |
| **SSE** | Web-tabanlı, streaming |
| **WebSocket** | Gerçek zamanlı, çift yönlü |

---

## 3. Araç Tasarım Prensipleri

### İyi Araç Tasarımı

| Prensip | Açıklama |
|---------|----------|
| Açık isim | Eylem odaklı (get_weather, create_user) |
| Tek amaç | Tek bir şeyi iyi yap |
| Doğrulanmış girdi | Tipler ve açıklamalarla şema |
| Yapılandırılmış çıktı | Öngörülebilir yanıt formatı |

### Girdi Şema Tasarımı

| Alan | Gerekli mi? |
|------|-------------|
| Type | Evet - object |
| Properties | Her parametreyi tanımla |
| Required | Zorunlu parametreleri listele |
| Description | İnsan tarafından okunabilir |

---

## 4. Kaynak Desenleri

### Kaynak Tipleri

| Tip | Kullanım |
|-----|----------|
| Static | Sabit veri (config, docs) |
| Dynamic | İstek üzerine oluşturulur |
| Template | Parametreli URI |

### URI Desenleri

| Desen | Örnek |
|-------|-------|
| Sabit | `docs://readme` |
| Parametreli | `users://{userId}` |
| Koleksiyon | `files://project/*` |

---

## 5. Hata Yönetimi

### Hata Tipleri

| Durum | Yanıt |
|-------|-------|
| Geçersiz parametreler | Doğrulama hata mesajı |
| Bulunamadı | Açık "bulunamadı" |
| Sunucu hatası | Genel hata, detayları logla |

### En İyi Uygulamalar

- Yapılandırılmış hatalar döndür
- Dahili detayları açığa çıkarma
- Hata ayıklama için logla
- Eylem yapılabilir mesajlar sağla

---

## 6. Multimodal İşleme

### Desteklenen Tipler

| Tip | Kodlama |
|-----|----------|
| Metin | Düz metin |
| Görseller | Base64 + MIME tipi |
| Dosyalar | Base64 + MIME tipi |

---

## 7. Güvenlik Prensipleri

### Girdi Doğrulama

- Tüm araç girdilerini doğrula
- Kullanıcı tarafından sağlanan verileri temizle
- Kaynak erişimini sınırla

### API Anahtarları

- Ortam değişkenlerini kullan
- Sırları loglama
- İzinleri doğrula

---

## 8. Yapılandırma

### Claude Desktop Config

| Alan | Amaç |
|------|------|
| command | Çalıştırılacak yürütülebilir |
| args | Komut argümanları |
| env | Ortam değişkenleri |

---

## 9. Test Etme

### Test Kategorileri

| Tip | Odak |
|-----|------|
| Unit | Araç mantığı |
| Integration | Tam sunucu |
| Contract | Şema doğrulama |

---

## 10. En İyi Uygulamalar Kontrol Listesi

- [ ] Açık, eylem odaklı araç isimleri
- [ ] Açıklamalı eksiksiz girdi şemaları
- [ ] Yapılandırılmış JSON çıktısı
- [ ] Tüm durumlar için hata yönetimi
- [ ] Girdi doğrulama
- [ ] Ortam tabanlı yapılandırma
- [ ] Hata ayıklama için loglama

---

> **Unutma:** MCP araçları basit, odaklı ve iyi belgelenmiş olmalıdır. AI, onları doğru kullanmak için açıklamalara güvenir.
