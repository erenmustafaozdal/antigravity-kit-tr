---
description: Projeler ve özellikler için yapılandırılmış beyin fırtınası. Uygulamadan önce birden fazla seçeneği araştırır.
---

# /brainstorm - Yapılandırılmış Fikir Keşfi

$ARGUMENTS

---

## Amaç

Bu komut, yapılandırılmış fikir keşfi için BEYİN FIRTINASI modunu etkinleştirir. Bir uygulamaya başlamadan önce seçenekleri keşfetmeniz gerektiğinde kullanın.

---

## Davranış

`/brainstorm` tetiklendiğinde:

1. **Hedefi Anla**
   - Hangi sorunu çözüyoruz?
   - Kullanıcı kim?
   - Hangi kısıtlamalar mevcut?

2. **Seçenekler Oluştur**
   - En az 3 farklı yaklaşım sun
   - Her birinin artılarını ve eksilerini belirt
   - Alışılmadık çözümleri de değerlendir

3. **Karşılaştır ve Tavsiye Et**
   - Takasları (trade-offs) özetle
   - Gerekçesiyle birlikte bir tavsiyede bulun

---

## Çıktı Formatı

```markdown
## 🧠 Beyin Fırtınası: [Konu]

### Bağlam
[Kısa sorun ifadesi]

---

### Seçenek A: [İsim]
[Açıklama]

✅ **Artılar:**
- [fayda 1]
- [fayda 2]

❌ **Eksiler:**
- [dezavantaj 1]

📊 **Efor:** Düşük | Orta | Yüksek

---

### Seçenek B: [İsim]
[Açıklama]

✅ **Artılar:**
- [fayda 1]

❌ **Eksiler:**
- [dezavantaj 1]
- [dezavantaj 2]

📊 **Efor:** Düşük | Orta | Yüksek

---

### Seçenek C: [İsim]
[Açıklama]

✅ **Artılar:**
- [fayda 1]

❌ **Eksiler:**
- [dezavantaj 1]

📊 **Efor:** Düşük | Orta | Yüksek

---

## 💡 Tavsiye

**Seçenek [X]** çünkü [gerekçe].

Hangi yönü keşfetmek istersiniz?
```

---

## Örnekler

```
/brainstorm kimlik doğrulama sistemi
/brainstorm karmaşık form için durum yönetimi
/brainstorm sosyal uygulama için veritabanı şeması
/brainstorm önbelleğe alma stratejisi
```

---

## Temel Prensipler

- **Kod yok** - bu fikirlerle ilgilidir, uygulama ile değil
- **Yardımcı olduğunda görselleştir** - mimari için diyagramlar kullan
- **Dürüst takaslar** - karmaşıklığı gizleme
- **Kullanıcıya bırak** - seçenekleri sun, kararı kullanıcı versin
