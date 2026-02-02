---
name: testing-patterns
description: Test desenleri ve prensipleri. Birim testleri (unit), entegrasyon testleri, mocking stratejileri.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Test Desenleri (Testing Patterns)

> Güvenilir test paketleri için prensipler.

---

## 1. Test Piramidi (Testing Pyramid)

```
        /\          E2E (Az)
       /  \         Kritik akışlar
      /----\
     /      \       Entegrasyon (Orta)
    /--------\      API, DB sorguları
   /          \
  /------------\    Birim (Çok)
                    Fonksiyonlar, sınıflar
```

---

## 2. AAA Deseni

| Adım | Amaç |
|------|------|
| **Arrange (Hazırla)** | Test verilerini kurma |
| **Act (Uygula)** | Test edilen kodu çalıştır |
| **Assert (Kontrol Et)** | Sonucu doğrula |

---

## 3. Test Türü Seçimi

### Her Birinin Ne Zaman Kullanılacağı

| Tür | En Uygun Durum | Hız |
|-----|----------------|-----|
| **Birim (Unit)** | Saf fonksiyonlar, mantık | Hızlı (< 50ms) |
| **Entegrasyon (Integration)** | API, DB, servisler | Orta |
| **E2E (Uçtan Uca)** | Kritik kullanıcı akışları | Yavaş |

---

## 4. Birim Test Prensipleri

### İyi Birim Testleri

| Prensip | Anlamı |
|---------|--------|
| Hızlı (Fast) | < 100ms per test |
| İzole (Isolated) | Dış bağımlılık yok |
| Tekrarlanabilir (Repeatable) | Her zaman aynı sonuç |
| Kendi Kendini Kontrol Eden (Self-checking) | Manuel doğrulama yok |
| Zamanında (Timely) | Kod ile birlikte yazılır |

### Neyi Birim Test Yapmalı?

| Test Et | Test Etme |
|---------|-----------|
| İş mantığı | Framework kodu |
| Uç durumlar (edge cases) | Üçüncü parti kütüphaneler |
| Hata yönetimi | Basit getter'lar |

---

## 5. Entegrasyon Test Prensipleri

### Neyi Test Etmeli?

| Alan | Odak |
|------|------|
| API uç noktaları | İstek/yanıt |
| Veritabanı | Sorgular, işlemler (transactions) |
| Dış servisler | Sözleşmeler (contracts) |

### Kurulum/Temizlik (Setup/Teardown)

| Aşama | Eylem |
|-------|--------|
| Before All | Kaynakları bağla |
| Before Each | Durumu sıfırla |
| After Each | Temizle |
| After All | Bağlantıları kes |

---

## 6. Mocking Prensipleri

### Ne Zaman Mock Yapılmalı?

| Mock Yap | Mock Yapma |
|----------|------------|
| Dış API'ler | Test edilen kod |
| Veritabanı (birim testinde) | Basit bağımlılıklar |
| Zaman/rastgele | Saf fonksiyonlar (pure functions) |
| Ağ | Bellekteki depolar (in-memory stores) |

### Mock Türleri

| Tür | Kullanım |
|-----|----------|
| Stub | Sabit değerler döndürür |
| Spy | Çağrıları takip eder |
| Mock | Beklentileri ayarlar |
| Fake | Basitleştirilmiş uygulama |

---

## 7. Test Organizasyonu

### İsimlendirme

| Desen | Örnek |
|-------|-------|
| Davranış odaklı | "kullanıcı bulunamadığında hata döndürmeli" |
| Şart odaklı | "kullanıcı bulunamadığında..." |
| Given-when-then | "X verildiğinde, Y yapıldığında, Z olmalı" |

### Gruplama

| Seviye | Kullanım |
|--------|----------|
| describe | İlgili testleri grupla |
| it/test | Tekil durum |
| beforeEach | Ortak kurulum |

---

## 8. Test Verisi

### Stratejiler

| Yaklaşım | Kullanım |
|----------|----------|
| Factory'ler | Test verisi üret |
| Fixture'lar | Önceden tanımlı veri kümeleri |
| Builder'lar | Akıcı nesne oluşturma (fluent object creation) |

### Prensipler

- Gerçekçi veri kullan
- Önemsiz olmayan değerleri rastgeleleştir (faker)
- Ortak fixture'ları paylaş
- Veriyi minimal tut

---

## 9. En İyi Pratikler

| Pratik | Neden? |
|--------|--------|
| Test başına bir assert | Net hata nedeni |
| Bağımsız testler | Sıra bağımlılığı olmaması |
| Hızlı testler | Sık sık çalıştırılabilir |
| Açıklayıcı isimler | Kendi kendini belgeler |
| Temizlik | Yan etkilerden kaçın |

---

## 10. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ Yapma | ✅ Yap |
|----------|--------|
| Uygulamayı (implementation) test et | Davranışı (behavior) test et |
| Test kodunu tekrarla | Factory kullan |
| Karmaşık test kurulumu | Basitleştir veya böl |
| Düzensiz testleri görmezden gel | Kök nedeni düzelt |
| Temizliği atla | Durumu sıfırla |

---

> **Unutmayın:** Testler dokümantasyondur. Birisi testlerden kodun ne yaptığını anlayamıyorsa, testleri yeniden yazın.
