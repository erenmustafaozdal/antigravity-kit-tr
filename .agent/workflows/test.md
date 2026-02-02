---
description: Test oluşturma ve test çalıştırma komutu. Kod için testler oluşturur ve yürütür.
---

# /test - Test Oluşturma ve Yürütme

$ARGUMENTS

---

## Amaç

Bu komut; testler oluşturur, mevcut testleri çalıştırır veya test kapsamını (coverage) kontrol eder.

---

## Alt Komutlar

```
/test                - Tüm testleri çalıştır
/test [dosya/özellik] - Belirli bir hedef için testler oluştur
/test coverage       - Test kapsam raporunu göster
/test watch          - Testleri izleme (watch) modunda çalıştır
```

---

## Davranış

### Test Oluşturma

Bir dosya veya özellik için test istendiğinde:

1. **Kodu Analiz Et**
   - Fonksiyonları ve metotları belirle
   - Uç durumları (edge cases) bul
   - Mock'lanacak bağımlılıkları tespit et

2. **Test Senaryoları Oluştur**
   - Başarılı durum (happy path) testleri
   - Hata durumları
   - Uç durumlar
   - Entegrasyon testleri (gerekirse)

3. **Testleri Yaz**
   - Projenin test framework'ünü (Jest, Vitest vb.) kullan
   - Mevcut test desenlerini takip et
   - Harici bağımlılıkları mock'la

---

## Çıktı Formatı

### Test Oluşturma İçin

```markdown
## 🧪 Testler: [Hedef]

### Test Planı
| Test Senaryosu | Tür | Kapsam |
|-----------|------|----------|
| Kullanıcı oluşturulmalı | Unit | Happy path |
| Geçersiz e-posta reddedilmeli | Unit | Validation |
| Veritabanı hatası yönetilmeli | Unit | Error case |

### Oluşturulan Testler

`tests/[dosya].test.ts`

[Testleri içeren kod bloğu]

---

Çalıştırmak için: `npm test`
```

### Test Yürütme İçin

```
🧪 Testler çalıştırılıyor...

✅ auth.test.ts (5 geçti)
✅ user.test.ts (8 geçti)
❌ order.test.ts (2 geçti, 1 kaldı)

Başarısız:
  ✗ should calculate total with discount
    Beklenen: 90
    Gelen: 100

Toplam: 15 test (14 geçti, 1 kaldı)
```

---

## Örnekler

```
/test src/services/auth.service.ts
/test kullanıcı kayıt akışı
/test coverage
/test fix failed tests
```

---

## Test Desenleri

### Unit Test Yapısı

```typescript
describe('AuthService', () => {
  describe('login', () => {
    it('geçerli bilgilerle token döndürmeli', async () => {
      // Arrange (Düzenle)
      const credentials = { email: 'test@test.com', password: 'pass123' };
      
      // Act (Çalıştır)
      const result = await authService.login(credentials);
      
      // Assert (Doğrula)
      expect(result.token).toBeDefined();
    });

    it('geçersiz şifre için hata fırlatmalı', async () => {
      // Arrange (Düzenle)
      const credentials = { email: 'test@test.com', password: 'wrong' };
      
      // Act & Assert (Çalıştır ve Doğrula)
      await expect(authService.login(credentials)).rejects.toThrow('Invalid credentials');
    });
  });
});
```

---

## Temel Prensipler

- **Uygulamayı değil, davranışı test et**
- **Test başına bir doğrulama (assertion)** (pratik olduğu sürece)
- **Açıklayıcı test isimleri**
- **Arrange-Act-Assert deseni**
- **Harici bağımlılıkları mock'la**
