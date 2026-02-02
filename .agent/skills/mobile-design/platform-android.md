# Android Platform Yönergeleri

> Material Design 3 (M3) temelleri, Android tasarım kuralları, Roboto tipografisi ve yerel (native) desenler.
> **Android cihazlar için geliştirme yaparken bu dosyayı okuyun.**

---

## 1. Material Design 3 Felsefesi

### Temel Material Prensipleri

```
METAFOR OLARAK MATERYAL:
├── Yüzeyler 3D uzayda var olur
├── Işık ve gölge hiyerarşiyi tanımlar
├── Hareket (Motion) süreklilik sağlar
└── Cesur, grafiksel ve amaca yönelik tasarım

ADAPTİF TASARIM:
├── Cihaz yeteneklerine yanıt verir
├── Tüm form faktörleri için tek bir UI
├── Duvar kağıdından gelen dinamik renk (Material You)
└── Kullanıcıya göre kişiselleştirilmiş

VARSAYILAN OLARAK ERİŞİLEBİLİR:
├── Büyük dokunmatik hedefler
├── Net görsel hiyerarşi
├── Semantik renkler
└── Hareket (Motion) tercihlere saygı duyar
```

### Material Design Değerleri

| Değer | Uygulama |
|-------|----------------|
| **Dinamik Renk** | Renkler duvar kağıdına/kullanıcı tercihine uyum sağlar |
| **Kişiselleştirme** | Kullanıcıya özel temalar |
| **Erişilebilirlik** | Her bileşenin içine yerleştirilmiştir |
| **Duyarlılık** | Tüm ekran boyutlarında çalışır |
| **Tutarlılık** | Birleştirilmiş tasarım dili |

---

## 2. Android Tipografisi

### Roboto Yazı Tipi Ailesi
- **Roboto:** Varsayılan sans-serif.
- **Roboto Flex:** Değişken (variable) font (API 33+).
- **Google Sans:** Google ürünleri için (özel lisanslı).

### Ölçeklenebilir Pikseller (sp)

```
sp = Ölçekten bağımsız pikseller (Scale-independent pixels)

sp şunlarla otomatik olarak ölçeklenir:
├── Kullanıcının yazı tipi boyutu tercihi
├── Ekran yoğunluğu (density)
└── Erişilebilirlik ayarları

KURAL: Metinler için HER ZAMAN sp, diğer her şey için dp kullanın.
```

---

## 3. Material Renk Sistemi

### Dinamik Renk (Material You)
Uygulamanız kullanıcının duvar kağıdından çıkarılan renk paletine (Primary, Secondary, Tertiary) otomatik olarak uyum sağlamalıdır.

### Karanlık Tema (Dark Theme)
- **Arka plan:** #121212 (varsayılan olarak tam siyah değildir).
- **Yükseklik (Elevation):** Daha yüksek elemanlar daha açık tonlu katmanlar (overlay) alır.

---

## 4. Android Düzen ve Boşluklar (Layout & Spacing)

### 8dp Temel Izgara (Grid)
Tüm boşluklar 8dp'nin katları olmalıdır:
- **4dp:** Bileşen içi (yarım adım).
- **8dp:** Minimum boşluk.
- **16dp:** Standart boşluk.
- **24dp/32dp:** Bölüm ve büyük boşluklar.

---

## 5. Android Navigasyon Desenleri

### Navigasyon Bileşenleri
- **Bottom Navigation:** 3-5 ana hedef için alt kısım.
- **Navigation Rail:** Tabletler ve katlanabilir cihazlar için sol dikey bar.
- **Navigation Drawer:** Çok sayıda hedef için açılır yan menü.
- **Top App Bar:** Mevcut bağlam ve eylemler için üst bar.

### Geri (Back) Navigasyonu
- **Geri butonu** veya **Geri jestini** (kenardan kaydırma) destekleyin.
- **Predictive Back (Öngörülü Geri):** Android 14+ ile gelen yeni animasyonu destekleyin.
- **Asla geri tuşunu beklenmedik şekilde engellemeyin.**

---

## 6. Material Bileşenleri

### Butonlar
- **Filled Button:** Birincil eylem.
- **Tonal Button:** İkincil eylem.
- **Outlined Button:** Üçüncül eylem.
- **Text Button:** En düşük vurgu.
- **Minimum dokunma hedefi:** 48dp (görsel daha küçük olsa bile).

### Floating Action Button (FAB)
Ekranın sağ altında, içeriğin üzerinde yüzen ana eylem butonu.

---

## 7. Android-Özgü Desenler

### Snackbar
Ekranın altında, navigasyonun üzerinde çıkan kısa süreli mesajlar. Tek bir metin eylemi içerebilir.

### Ripple (Dalgalanma) Efekti
HER dokunulabilir öğe, dokunulduğunda bir dalgalanma efektine sahip olmalıdır. Bu, "Android hissi" için ZORUNLUDUR.

### Çek-Yenile (Pull to Refresh)
Material dairesel ilerleme göstergesi (circular progress indicator) ile yukarıdan aşağı çekme hareketi.

---

## 8. Material Sembolleri
Google'ın ikon kütüphanesidir. `Outlined` (varsayılan), `Rounded` ve `Sharp` stilleri mevcuttur.

---

## 9. Android Erişilebilirlik (Accessibility)

- **TalkBack:** Her etkileşimli öğeye `contentDescription` ekleyin.
- **Dokunma Hedefi:** Minimum 48dp x 48dp.
- **Yazı Tipi Ölçekleme:** UI'ınızı %200 yazı tipi boyutunda test edin.

---

## 10. Android Kontrol Listesi

- [ ] **Material 3 bileşenleri kullanılıyor mu?**
- [ ] **Dokunma hedefleri ≥ 48dp mi?**
- [ ] **Tüm dokunulabilir öğelerde Ripple efekti var mı?**
- [ ] **Dinamik renk desteği var mı?**
- [ ] **Geri navigasyonu (Back) doğru çalışıyor mu?**
- [ ] **TalkBack ile test edildi mi?**

---

> **Unutma:** Android kullanıcıları Material Design bekler. Material desenlerini yoksayan özel tasarımlar yabancı ve "bozuk" hissettirir. Material bileşenlerini temel olarak kullanın ve üzerine düşünerek özelleştirin.
