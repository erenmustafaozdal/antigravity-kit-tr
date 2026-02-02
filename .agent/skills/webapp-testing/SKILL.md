---
name: webapp-testing
description: Web uygulaması test etme prensipleri. E2E, Playwright, derin denetim stratejileri.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Web Uygulaması Test Etme (Web App Testing)

> Her şeyi keşfet ve test et. Test edilmemiş rota bırakma.

## 🔧 Çalışma Zamanı Script'leri

**Otomatik tarayıcı testi için bunları çalıştırın:**

| Script | Amaç | Kullanım |
|--------|------|----------|
| `scripts/playwright_runner.py` | Temel tarayıcı testi | `python scripts/playwright_runner.py https://example.com` |
| | Ekran görüntüsüyle | `python scripts/playwright_runner.py <url> --screenshot` |
| | Erişilebilirlik kontrolü | `python scripts/playwright_runner.py <url> --a11y` |

**Gerekli:** `pip install playwright && playwright install chromium`

---

## 1. Derin Denetim Yaklaşımı

### Önce Keşif

| Hedef | Nasıl Bulunur |
|-------|---------------|
| Rotalar | app/, pages/, router dosyalarını tara |
| API uç noktaları | HTTP metodları için grep |
| Componentler | Component dizinlerini bul |
| Özellikler | Dokümantasyonu oku |

### Sistematik Test Etme

1. **Haritalama** - Tüm rota/API'leri listele
2. **Tarama** - Yanıt verdiğini doğrula
3. **Test Etme** - Kritik yolları kapsa

---

## 2. Web İçin Test Piramidi

```
        /\          E2E (Az)
       /  \         Kritik kullanıcı akışları
      /----\
     /      \       Entegrasyon (Bazı)
    /--------\      API, veri akışı
   /          \
  /------------\    Component (Çok)
                    Bireysel UI parçaları
```

---

## 3. E2E Test Prensipleri

### Neyi Test Etmeli

| Öncelik | Testler |
|---------|---------|
| 1 | Mutlu yol kullanıcı akışları |
| 2 | Kimlik doğrulama akışları |
| 3 | Kritik iş eylemleri |
| 4 | Hata yönetimi |

### E2E En İyi Uygulamalar

| Uygulama | Neden |
|---------| ------|
| data-testid kullan | Stabil seçiciler |
| Elementleri bekle | Kararsız testlerden kaçın |
| State'i temizle | Bağımsız testler |
| İmplementasyon detaylarından kaçın | Kullanıcı davranışını test et |

---

## 4. Playwright Prensipleri

### Temel Kavramlar

| Kavram | Kullanım |
|--------|----------|
| Page Object Model | Sayfa mantığını kapsülle |
| Fixtures | Yeniden kullanılabilir test kurulumu |
| Assertions | Dahili otomatik bekleme |
| Trace Viewer | Başarısızlıkları debug et |

### Yapılandırma

| Ayar | Öneri |
|------|-------|
| Retries | CI'da 2 |
| Trace | on-first-retry |
| Screenshots | on-failure |
| Video | retain-on-failure |

---

## 5. Görsel Test Etme

### Ne Zaman Kullanılır

| Senaryo | Değer |
|---------|-------|
| Tasarım sistemi | Yüksek |
| Pazarlama sayfaları | Yüksek |
| Component kütüphanesi | Orta |
| Dinamik içerik | Düşük |

### Strateji

- Baseline ekran görüntüleri
- Değişikliklerde karşılaştır
- Görsel farkları incele
- Kasıtlı değişiklikleri güncelle

---

## 6. API Test Etme Prensipleri

### Kapsam Alanları

| Alan | Testler |
|------|---------|
| Durum kodları | 200, 400, 404, 500 |
| Yanıt şekli | Şema ile eşleşir |
| Hata mesajları | Kullanıcı dostu |
| Uç durumlar | Boş, büyük, özel karakterler |

---

## 7. Test Organizasyonu

### Dosya Yapısı

```
tests/
├── e2e/           # Tam kullanıcı akışları
├── integration/   # API, veri
├── component/     # UI birimleri
└── fixtures/      # Paylaşılan veri
```

### İsimlendirme Konvansiyonu

| Desen | Örnek |
|-------|-------|
| Özellik-tabanlı | `login.spec.ts` |
| Açıklayıcı | `user-can-checkout.spec.ts` |

---

## 8. CI Entegrasyonu

### Pipeline Adımları

1. Bağımlılıkları kur
2. Tarayıcıları kur
3. Testleri çalıştır
4. Artifact'leri yükle (trace'ler, ekran görüntüleri)

### Paralelleştirme

| Strateji | Kullanım |
|----------|----------|
| Dosya başına | Playwright varsayılan |
| Sharding | Büyük suit'ler |
| Workers | Birden fazla tarayıcı |

---

## 9. Anti-Desenler

| ❌ Yapma | ✅ Yap |
|----------|--------|
| İmplementasyonu test et | Davranışı test et |
| Sabit beklemeleri kodla | Otomatik bekleme kullan |
| Temizlemeyi atla | Testleri izole et |
| Kararsız testleri görmezden gel | Kök nedeni düzelt |

---

> **Unutma:** E2E testleri pahalıdır. Yalnızca kritik yollar için kullan.
