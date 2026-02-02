---
description: Hata ayıklama komutu. Sistematik sorun incelemesi için HATA AYIKLAMA (DEBUG) modunu etkinleştirir.
---

# /debug - Sistematik Sorun İncelemesi

$ARGUMENTS

---

## Amaç

Bu komut; sorunların, hataların veya beklenmedik davranışların sistematik olarak incelenmesi için HATA AYIKLAMA modunu etkinleştirir.

---

## Davranış

`/debug` tetiklendiğinde:

1. **Bilgi Topla**
   - Hata mesajı
   - Yeniden oluşturma (reproduction) adımları
   - Beklenen ve gerçekleşen davranış
   - Son değişiklikler

2. **Hipotezler Kur**
   - Olası nedenleri listele
   - Olasılık sırasına diz

3. **Sistematik Olarak İncele**
   - Her hipotezi test et
   - Logları ve veri akışını kontrol et
   - Eleme yöntemini kullan

4. **Düzelt ve Önle**
   - Düzeltmeyi uygula
   - Kök nedeni açıkla
   - Önleyici tedbirler ekle

---

## Çıktı Formatı

```markdown
## 🔍 Hata Ayıklama: [Sorun]

### 1. Belirti
[Ne oluyor?]

### 2. Toplanan Bilgiler
- Hata: `[hata mesajı]`
- Dosya: `[dosya yolu]`
- Satır: [satır numarası]

### 3. Hipotezler
1. ❓ [En olası neden]
2. ❓ [İkinci olasılık]
3. ❓ [Daha düşük olasılıklı neden]

### 4. İnceleme

**Hipotez 1 Test Ediliyor:**
[Ne kontrol ettim] → [Sonuç]

**Hipotez 2 Test Ediliyor:**
[Ne kontrol ettim] → [Sonuç]

### 5. Kök Neden
🎯 **[Bunun neden olduğuna dair açıklama]**

### 6. Düzeltme
```[dil]
// Önce
[bozuk kod]

// Sonra
[düzeltilmiş kod]
```

### 7. Önleme
🛡️ [Bunun gelecekte tekrar etmesi nasıl önlenir?]
```

---

## Örnekler

```
/debug giriş çalışmıyor
/debug API 500 hatası döndürüyor
/debug form gönderilmiyor
/debug veriler kaydedilmiyor
```

---

## Temel Prensipler

- **Varsaymadan önce sor** - tam hata bağlamını al
- **Hipotezleri test et** - rastgele tahminlerde bulunma
- **Nedenini açıkla** - sadece neyin düzeltileceğini değil
- **Tekrarı önle** - testler ve doğrulama ekle
