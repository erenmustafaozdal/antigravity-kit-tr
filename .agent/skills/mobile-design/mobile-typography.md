# Mobil Tipografi Referansı

> Yazı tipi ölçeği, sistem fontları, Dynamic Type, erişilebilirlik ve karanlık mod tipografisi.
> **Tipografi hataları, okunamaz mobil uygulamaların 1 numaralı nedenidir.**

---

## 1. Mobil Tipografi Temelleri

### Mobil Tipografi Neden Farklıdır?

```
MASAÜSTÜ:                        MOBİL:
├── 50-75 cm izleme mesafesi     ├── 30-40 cm izleme mesafesi
├── Geniş ekran                  ├── Küçük ve dar ekran
├── Detaylar için hover          ├── Detaylar için dokunma/kaydırma
├── Kontrollü ışık               ├── Değişken ışık (dış mekan vb.)
├── Sabit font boyutu            ├── Kullanıcı kontrollü boyutlandırma
└── Uzun okuma seansları         └── Hızlı tarama (scanning)
```

### Mobil Tipografi Kuralları

| Kural | Masaüstü | Mobil |
|------|---------|--------|
| **Minimum gövde boyutu** | 14px | 16px (14pt/14sp) |
| **Maksimum satır uzunluğu**| 75 karakter | 40-60 karakter |
| **Satır yüksekliği** | 1.4-1.5 | 1.4-1.6 (daha cömert) |
| **Kontrast** | AA (4.5:1) | AA minimum, AAA tercih edilir |

---

## 2. Sistem Fontları

### iOS: SF Pro Ailesi
- **SF Pro Display:** Büyük metinler (≥ 20pt).
- **SF Pro Text:** Gövde metni (< 20pt).
- **Özellikler:** Optik boyutlandırma, dinamik aralık (tracking) ve mükemmel okunabilirlik.

### Android: Roboto Ailesi
- **Roboto:** Varsayılan sans-serif.
- **Roboto Flex:** Değişken font.
- **Özellikler:** Ekranlar için optimize edilmiş, geniş dil desteği.

---

## 3. Yazı Tipi Ölçeği (Type Scale)

### iOS ve Android Ölçekleri
Her iki platformun da kendine özgü (`Large Title`, `Headline`, `Body`, `Display`, `Label` vb.) hazır ölçekleri vardır. Bu ölçekleri kullanmak, uygulama genelinde tutarlılık ve yerel his (native feel) sağlar.

---

## 4. Dynamic Type / Metin Ölçekleme

### ZORUNLU Desteği
- **iOS:** Sistem ayarlarından yazı tipi boyutunu değiştiren kullanıcılar için `Dynamic Type` desteği zorunludur.
- **Android:** Her zaman `sp` (Scale-independent pixels) birimini kullanın. Kullanıcılar yazı tipi boyutunu %85'ten %200'e kadar ölçekleyebilir.

> 🔴 **KURAL:** UI'ınızı HER ZAMAN %200 yazı tipi boyutunda test edin. Metinlerin taşmadığından ve okunabilir kaldığından emin olun.

---

## 5. Tipografi Erişilebilirliği

- **Minimum boyutlar:** Gövde metni için 16px, ikincil metinler için 14px önerilir. 11px altındaki hiçbir şeyi kullanmayın.
- **Kontrast:** Görme zorluğu çekenler ve güneş ışığı altındaki kullanımlar için en az 4.5:1 kontrast oranını (WCAG AA) yakalayın.

---

## 6. Karanlık Mod Tipografisi

- **Saf beyaz kullanmayın:** Karanlık arka planda saf beyaz (#FFF) göz yorar. Hafif kırık beyaz (#E0E0E0 - #F0F0F0) tercih edin.
- **Kalınlık (Weight):** Karanlık modda ışık dağılması nedeniyle metinler daha ince görünebilir. Gerekirse orta (medium) kalınlık kullanın.

---

## 7. Tipografi Kontrol Listesi

- [ ] **Gövde metni ≥ 16px/pt/sp mi?**
- [ ] **Satır uzunluğu ≤ 60 karakter mi?**
- [ ] **iOS'ta Dynamic Type test edildi mi?**
- [ ] **Android'de %200 font ölçeği kontrol edildi mi?**
- [ ] **Güneş ışığı altında okunabilirlik yeterli mi?**
- [ ] **Karanlık mod kontrastı uygun mu?**

---

> **Unutma:** Eğer kullanıcılar metni okuyamıyorsa, uygulamanız bozuktur. Tipografi bir süsleme değil, arayüzün temelidir. Gerçek cihazlarda, gerçek koşullarda ve erişilebilirlik ayarları açıkken test edin.
