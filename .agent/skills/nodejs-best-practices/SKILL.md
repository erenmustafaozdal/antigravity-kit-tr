---
name: nodejs-best-practices
description: Node.js geliştirme prensipleri ve karar verme. Framework seçimi, async desenleri, güvenlik ve mimari. Düşünmeyi öğretir, kopyalamayı değil.
allowed-tools: Read, Write, Edit, Glob, Grep
---

# Node.js En İyi Pratikleri

> 2025 yılı için Node.js geliştiriminde prensipler ve karar verme.
> **Kod desenleri ezberlemek değil, DÜŞÜNMEYİ öğrenin.**

---

## ⚠️ Bu Yetenek Nasıl Kullanılır?

Bu yetenek, kopyalanacak sabit kodu değil, **karar verme prensipl

erini** öğretir.

- Belirsiz durumlarda kullanıcıya tercihlerini SORUN
- Framework/deseni BAĞLAM'a göre seçin
- Her seferinde aynı çözümü varsayılan yapmayın

---

## 1. Framework Seçimi (2025)

### Karar Ağacı

```
Ne inşa ediyorsunuz?
│
├── Edge/Serverless (Cloudflare, Vercel)
│   └── Hono (sıfır bağımlılık, ultra hızlı soğuk başlatma)
│
├── Yüksek Performanslı API
│   └── Fastify (Express'ten 2-3x daha hızlı)
│
├── Kurumsal/Ekip aşinalığı
│   └── NestJS (yapılandırılmış, DI, decorator'lar)
│
├── Legacy/Stabil/Maksimum ekosistem
│   └── Express (olgun, en fazla middleware)
│
└── Frontend ile tam yığın (full-stack)
    └── Next.js API Routes veya tRPC
```

### Karşılaştırma Prensipleri

| Faktör | Hono | Fastify | Express |
|--------|------|---------|---------|
| **En uygun** | Edge, serverless | Performans | Legacy, öğrenme |
| **Soğuk başlatma** | En hızlı | Hızlı | Orta |
| **Ekosistem** | Büyüyen | İyi | En geniş |
| **TypeScript** | Yerel (Native) | Mükemmel | İyi |
| **Öğrenme eğrisi** | Düşük | Orta | Düşük |

### Sorulması Gereken Seçim Soruları:
1. Dağıtım hedefi nedir?
2. Soğuk başlatma süresi kritik mi?
3. Ekibin mevcut deneyimi var mı?
4. Bakımı yapılacak legacy kod var mı?

---

## 2. Runtime Hususları (2025)

### Yerel TypeScript (Native TypeScript)

```
Node.js 22+: --experimental-strip-types
├── .ts dosyalarını doğrudan çalıştır
├── Basit projeler için build adımı gerekmez
└── Şunlar için düşünün: scriptler, basit API'ler
```

### Modül Sistemi Kararı

```
ESM (import/export)
├── Modern standart
├── Daha iyi tree-shaking
├── Async modül yükleme
└── Kullanım: yeni projeler

CommonJS (require)
├── Legacy uyumluluk
├── Daha fazla npm paketi desteği
└── Kullanım: mevcut kod tabanları, bazı özel durumlar
```

### Runtime Seçimi

| Runtime | En Uygun Durum |
|---------|----------------|
| **Node.js** | Genel amaçlı, en geniş ekosistem |
| **Bun** | Performans, yerleşik bundler |
| **Deno** | Güvenlik odaklı, yerleşik TypeScript |

---

## 3. Mimari Prensipler

### Katmanlı Yapı Konsepti

```
İstek Akışı:
│
├── Controller/Route Katmanı
│   ├── HTTP özgülükleri ele alır
│   ├── Sınırda girdi doğrulaması
│   └── Servis katmanını çağırır
│
├── Servis Katmanı (Service Layer)
│   ├── İş mantığı
│   ├── Framework'ten bağımsız
│   └── Repository katmanını çağırır
│
└── Repository Katmanı
    ├── Yalnızca veri erişimi
    ├── Veritabanı sorguları
    └── ORM etkileşimleri
```

### Bu Neden Önemlidir:
- **Test Edilebilirlik**: Katmanları bağımsız olarak mock'layın
- **Esneklik**: İş mantığına dokunmadan veritabanını değiştirin
- **Netlik**: Her katmanın tek sorumluluğu vardır

### Ne Zaman Basitleştirmeli:
- Küçük scriptler → Tek dosya OK
- Prototip → Daha az yapı kabul edilebilir
- Her zaman sorun: "Bu büyüyecek mi?"

---

## 4. Hata Yönetimi Prensipleri

### Merkezi Hata Yönetimi

```
Desen:
├── Özel hata sınıfları oluştur
├── Herhangi bir katmandan fırlat
├── En üst düzeyde yakala (middleware)
└── Tutarlı yanıt formatı
```

### Hata Yanıtı Felsefesi

```
İstemci alır:
├── Uygun HTTP durumu
├── Programatik işleme için hata kodu
├── Kullanıcı dostu mesaj
└── Dahili detaylar YOK (güvenlik!)

Loglar alır:
├── Tam yığın izleme (full stack trace)
├── İstek bağlamı
├── Kullanıcı ID'si (varsa)
└── Zaman damgası
```

### Durum Kodu Seçimi

| Durum | HTTP Kodu | Ne Zaman |
|-------|-----------|----------|
| Kötü girdi | 400 | İstemci geçersiz veri gönderdi |
| Kimlik doğrulama yok | 401 | Eksik veya geçersiz kimlik bilgileri |
| İzin yok | 403 | Geçerli kimlik doğrulama, ama izin yok |
| Bulunamadı | 404 | Kaynak mevcut değil |
| Çakışma | 409 | Kopya veya durum çakışması |
| Doğrulama | 422 | Şema geçerli ama iş kuralları başarısız |
| Sunucu hatası | 500 | Bizim hatamız, her şeyi logla |

---

## 5. Async Des

en Prensipleri

### Her Birinin Ne Zaman Kullanılacağı

| Desen | Ne Zaman Kullanılır |
|-------|---------------------|
| `async/await` | Ardışık async işlemleri |
| `Promise.all` | Paralel bağımsız işlemler |
| `Promise.allSettled` | Bazıları başarısız olabilecek paralel işlemler |
| `Promise.race` | Timeout veya ilk yanıt kazanır |

### Event Loop Farkındalığı

```
I/O-bağımlı (I/O-bound) (async yardımcı olur):
├── Veritabanı sorguları
├── HTTP istekleri
├── Dosya sistemi
└── Ağ işlemleri

CPU-bağımlı (CPU-bound) (async yardımcı olmaz):
├── Kripto işlemleri
├── Görüntü işleme
├── Karmaşık hesaplamalar
└── → Worker thread'ler kullanın veya dış kaynak kullanın
```

### Event Loop Bloklama'dan Kaçınma

- Üretimde asla senkron metodları kullanmayın (fs.readFileSync, vb.)
- CPU-yoğun işleri dışarıya taşıyın
- Büyük veri için streaming kullanın

---

## 6. Doğrulama Prensipleri

### Sınırlarda Doğrula

```
Nerede doğrulanmalı:
├── API giriş noktası (request body/params)
├── Veritabanı işlemlerinden önce
├── Dış veri (API yanıtları, dosya yüklemeleri)
└── Ortam değişkenleri (başlangıç)
```

### Doğrulama Kütüphanesi Seçimi

| Kütüphane | En Uygun Durum |
|-----------|----------------|
| **Zod** | TypeScript öncelikli, çıkarım (inference) |
| **Valibot** | Daha küçük paket (tree-shakeable) |
| **ArkType** | Performans kritik |
| **Yup** | Mevcut React Form kullanımı |

### Doğrulama Felsefesi

- Hızlı başarısız ol: Erken doğrula
- Spesifik ol: Net hata mesajları
- Güvenme: "Dahili" veriye bile

---

## 7. Güvenlik Prensipleri

### Güvenlik Kontrol Listesi (Kod Değil)

- [ ] **Girdi doğrulaması**: Tüm girdiler doğrulandı
- [ ] **Parametreli sorgular**: SQL için string birleştirme yok
- [ ] **Şifre hashleme**: bcrypt veya argon2
- [ ] **JWT doğrulama**: Her zaman imza ve geçerlilik süresi doğrula
- [ ] **Hız sınırlama**: Kötüye kullanımdan koru
- [ ] **Güvenlik başlıkları**: Helmet.js veya eşdeğeri
- [ ] **HTTPS**: Üretimde her yerde
- [ ] **CORS**: Düzgün yapılandırılmış
- [ ] **Gizli bilgiler**: Yalnızca ortam değişkenleri
- [ ] **Bağımlılıklar**: Düzenli olarak denetlenmiş

### Güvenlik Zihniyeti

```
Hiçbir şeye güvenme:
├── Sorgu parametreleri → doğrula
├── İstek gövdesi → doğrula
├── Başlıklar → doğrula
├── Çerezler → doğrula
├── Dosya yüklemeleri → tara
└── Dış API'ler → yanıtı doğrula
```

---

## 8. Test Prensipleri

### Test Stratejisi Seçimi

| Tür | Amaç | Araçlar |
|-----|------|---------|
| **Birim (Unit)** | İş mantığı | node:test, Vitest |
| **Entegrasyon** | API uç noktaları | Supertest |
| **E2E** | Tam akışlar | Playwright |

### Neyi Test Etmeli (Öncelikler)

1. **Kritik yollar**: Kimlik doğrulama, ödemeler, temel iş
2. **Uç durumlar**: Boş girdiler, sınırlar
3. **Hata yönetimi**: İşler başarısız olduğunda ne olur?
4. **Test etmeye değmez**: Framework kodu, önemsiz getter'lar

### Yerleşik Test Çalıştırıcı (Node.js 22+)

```
node --test src/**/*.test.ts
├── Dış bağımlılık yok
├── İyi kapsam raporlaması
└── İzleme modu (watch mode) mevcut
```

---

## 10. Anti-Desenler (Kaçınılması Gerekenler)

### ❌ YAPMAYIN:
- Yeni edge projeleri için Express kullanmak (Hono kullanın)
- Üretim kodunda senkron metodlar kullanmak
- Controller'lara iş mantığı koymak
- Girdi doğrulamasını atlamak
- Gizli bilgileri hardcode etmek
- Doğrulama yapmadan dış verilere güvenmek
- Event loop'u CPU işi ile bloklamak

### ✅ YAPIN:
- Framework'ü bağlam

a göre seçin
- Belirsiz olduğunda kullanıcıya tercihlerini sorun
- Büyüyen projeler için katmanlı mimari kullanın
- Tüm girdileri doğrulayın
- Gizli bilgiler için ortam değişkenleri kullanın
- Optimize etmeden önce profilleme yapın

---

## 11. Karar Kontrol Listesi

Uygulamadan önce:

- [ ] **Kullanıcıya stack tercihi soruldu mu?**
- [ ] **BU bağlam için framework seçildi mi?** (sadece varsayılan değil)
- [ ] **Dağıtım hedefi değerlendirildi mi?**
- [ ] **Hata yönetimi stratejisi planlandı mı?**
- [ ] **Doğrulama noktaları belirlendi mi?**
- [ ] **Güvenlik gereksinimleri değerlendirildi mi?**

---

> **Unutmayın**: Node.js en iyi pratikleri, desen ezberlemekle değil, karar vermeyle ilgilidir. Her proje, gereksinimlerine göre yeni bir değerlendirmeyi hak eder.
