# Mobil Renk Sistemi Referansı

> OLED optimizasyonu, karanlık mod, pil duyarlı renkler ve dış mekan görünürlüğü.
> **Mobilde renk sadece estetik değildir; pil ömrü ve kullanılabilirlik demektir.**

---

## 1. Mobil Renk Temelleri

### Mobil Renk Neden Farklıdır?

```
MASAÜSTÜ:                           MOBİL:
├── LCD ekranlar (arkadan aydınlatmalı) ├── Yaygın OLED ekranlar
├── Kontrollü ışıklandırma          ├── Dış mekan, parlak güneş
├── Kararlı güç kaynağı             ├── Pil ömrü kritiktir
└── Statik izleme                   └── Değişken açılar, hareket
```

### Öncelikler
1. **Okunabilirlik:** Dış mekan ve değişken ışık koşulları.
2. **Pil Verimliliği:** OLED ekranlarda karanlık mod pil tasarrufu sağlar.
3. **Sistem Entegrasyonu:** Karanlık/aydınlık mod desteği.
4. **Semantik:** Hata, başarı, uyarı renklerinin netliği.

---

## 2. OLED Değerlendirmeleri

### OLED Nasıl Farklıdır?
LCD ekranlarda arka aydınlatma her zaman açıktır. OLED'de ise her piksel kendi ışığını yayar. Siyah piksel KAPALI demektir (sıfır güç tüketimi).

### Pil Tasarrufu
Rengin enerji tüketimi (oransal):
- **#000000 (Tam Siyah):** %0
- **#1A1A1A (Siyaha Yakın):** ~%15
- **#FFFFFF (Beyaz):** %100

> **ÖNERİ:** Arka planlar için #000000 (Tam Siyah), kartlar ve yüzeyler için #0D0D0D-#1A1A1A kullanın.

---

## 3. Karanlık Mod Tasarımı

### Renk Stratejisi
Aydınlık moddaki renkleri sadece tersine çevirmeyin (invert). Doygun renkler (saturated) karanlık modda göz yorabilir.
- **Metin:** Saf beyaz (#FFF) yerine kirli beyaz (#E0E0E0) kullanın.
- **Yüzey:** Eleman yükseldikçe (elevation) yüzey rengini hafifçe açın (shadow yerine renk tonuyla derinlik).

---

## 4. Dış Mekan Görünürlüğü
Güneş ışığı düşük kontrastı yok eder.
- **Minimum Kontrast:** Normal metin için 4.5:1 (WCAG AA). Önerilen 7:1+ (AAA).
- **Kaçının:** Beyaz üzerine açık gri metin, pastel renkler, düşük opaklıkta katmanlar.

---

## 5. Semantik Renkler
| Anlam | iOS | Android |
|----------|---------|-----------------|
| Hata | #FF3B30 | #B3261E |
| Başarı | #34C759 | #4CAF50 |
| Uyarı | #FF9500 | #FFC107 |

> **KURAL:** Asla sadece renge güvenmeyin; renk körü kullanıcılar için her zaman ikonlarla destekleyin.

---

## 6. Dinamik Renk (Material You - Android)
Android 12+ ile gelen özellik sayesinde uygulama, kullanıcının duvar kağıdından gelen renklere uyum sağlar.

---

## 7. Renk Kontrol Listesi

- [ ] **Karanlık ve aydınlık mod varyantları tanımlandı mı?**
- [ ] **Kontrast oranları kontrol edildi mi (en az 4.5:1)?**
- [ ] **OLED pil tasarrufu (tam siyah desteği) düşünüldü mü?**
- [ ] **Sadece renge dayalı olmayan göstergeler (ikonlar) var mı?**
- [ ] **Dış mekanda, parlak ışıkta test edildi mi?**

---

> **Unutma:** Mobilde renk en kötü koşullarda çalışmalıdır; parlak güneş, yorgun gözler, renk körlüğü ve düşük pil. Bu testleri geçemeyen güzel görünen renkler işe yaramazdır.
