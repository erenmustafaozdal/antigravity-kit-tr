# Tipografi Sistemi Referansı

> Tipografi prensipleri ve karar verme süreci - ezberlemeyi değil, düşünmeyi öğrenin.
> **Sabit yazı tipi isimleri veya boyutları yok - sistemi anlayın.**

---

## 1. Modüler Ölçek (Modular Scale) Prensipleri

### Modüler Ölçek Nedir?

```
Yazı boyutları arasındaki matematiksel ilişkidir:
├── Bir TEMEL (base) boyut seçin (genellikle gövde metni)
├── Bir ORAN (çarpan) seçin
└── Tüm boyutları şu formülle üretin: temel × oran^n
```

### Yaygın Oranlar ve Kullanım Alanları

| Oran | Değer | Hissi | En İyi Kullanım |
|-------|-------|---------|----------|
| Minor Second | 1.067 | Çok hafif | Yoğun arayüzler, küçük ekranlar |
| Major Second | 1.125 | Hafif | Kompakt arayüzler |
| Minor Third | 1.2 | Rahat | Mobil uygulamalar, kartlar |
| Major Third | 1.25 | Dengeli | Genel web (en yaygın) |
| Perfect Fourth | 1.333 | Belirgin | Editöryel içerik, bloglar |
| Perfect Fifth | 1.5 | Dramatik | Başlıklar, pazarlama sayfaları |
| Altın Oran | 1.618 | Maksimum etki | Hero bölümleri, büyük ekranlar |

### Ölçeğinizi Oluşturun

```
Verilen: temel = TEMEL_BOYUTUNUZ, oran = ORANINIZ

Ölçek:
├── xs:  temel ÷ oran²
├── sm:  temel ÷ oran
├── temel: TEMEL_BOYUTUNUZ
├── lg:  temel × oran
├── xl:  temel × oran²
├── 2xl: temel × oran³
├── 3xl: temel × oran⁴
└── ... gerektiği kadar devam edin
```

### Temel Boyut Seçimi

| Bağlam | Temel Boyut Aralığı | Neden? |
|---------|-----------------|-----|
| Mobil öncelikli | 16-18px | Küçük ekranlarda okunabilirlik |
| Masaüstü uygulama | 14-16px | Bilgi yoğunluğu ve verimlilik |
| Editöryel | 18-21px | Uzun okumalarda konfor |
| Erişilebilirlik odaklı| 18px+ | Daha kolay okuma |

---

## 2. Yazı Tipi Eşleştirme (Font Pairing) Prensipleri

### Yazı Tiplerini Birbirine Uygun Kılan Nedir?

```
Kontrast + Uyum:
├── Hiyerarşi yaratacak kadar FARKLI
├── Bütünlük hissi verecek kadar BENZER
└── Genellikle: serif + sans-serif, veya ekran fontu + nötr font
```

### Eşleştirme Stratejileri

| Strateji | Nasıl Yapılır | Sonuç |
|----------|-----|--------|
| **Kontrast** | Serif başlık + Sans gövde | Klasik, editöryel his |
| **Aynı Aile** | Tek bir değişken font, farklı ağırlıklar | Bütünsel, modern |
| **Aynı Tasarımcı** | Aynı dökümhaneden çıkan fontlar | Genellikle uyumlu oranlar |
| **Dönem Uyumu** | Aynı zaman dilimine ait fontlar | Tarihsel tutarlılık |

### Nelere Bakılmalı?

```
Eşleştirirken şunları karşılaştırın:
├── x-yüksekliği (küçük harflerin yüksekliği)
├── Harf genişliği (dar vs geniş)
├── Çizgi kontrastı (ince/kalın varyasyonu)
└── Genel ruh hali (resmi vs rahat)
```

### Güvenli Eşleştirme Desenleri

| Başlık Stili | Gövde Stili | Ruh Hali |
|---------------|------------|------|
| Geometrik sans | Humanist sans | Modern, cana yakın |
| Display serif | Temiz sans | Editöryel, sofistike |
| Nötr sans | Aynı sans | Minimal, teknolojik |
| Kalın geometrik | İnce geometrik | Çağdaş |

### Kaçınılması Gerekenler

- ❌ İki farklı dekoratif fontu birlikte kullanmak
- ❌ Birbiriyle çakışan birbirine çok benzer fontlar
- ❌ 2-3'ten fazla font ailesi kullanmak
- ❌ x-yükseklikleri çok farklı olan fontlar

---

## 3. Satır Yüksekliği (Line Height) Prensipleri

### İlişki Döngüsü

```
Satır yüksekliği şunlara bağlıdır:
├── Yazı boyutu (büyük metin = daha az satır yüksekliği)
├── Satır genişliği (uzun satırlar = daha fazla satır yüksekliği)
├── Yazı tipi tasarımı (bazı fontlar daha fazla alana ihtiyaç duyar)
└── İçerik türü (başlıklar vs gövde metni)
```

### Bağlama Göre Yönergeler

| İçerik Türü | Satır Yüksekliği Aralığı | Neden? |
|--------------|-------------------|-----|
| **Başlıklar** | 1.1 - 1.3 | Kısa satırlar, kompakt görünüm |
| **Gövde metni** | 1.4 - 1.6 | Rahat okuma |
| **Uzun yazılar** | 1.6 - 1.8 | Maksimum okunabilirlik |
| **Arayüz öğeleri**| 1.2 - 1.4 | Alan verimliliği |

### Ayarlama Faktörleri

- **Daha uzun satır genişliği** → Satır yüksekliğini artırın
- **Daha büyük yazı boyutu** → Satır yüksekliği oranını azaltın
- **Tamamı büyük harf** → Daha fazla satır yüksekliğine ihtiyaç duyabilir
- **Dar harf boşluğu (tracking)** → Daha fazla satır yüksekliği gerekebilir

---

## 4. Satır Genişliği (Line Length) Prensipleri

### En Uygun Okuma Genişliği

```
İdeal nokta: Satır başına 45-75 karakter
├── < 45: Çok kesik, akışı bozar
├── 45-75: Rahat okuma deneyimi
├── > 75: Göz takibini zorlaştırır ve yorar
```

### Nasıl Ölçülür?

```css
/* Karakter tabanlı (önerilen) */
max-width: 65ch; /* ch = "0" karakterinin genişliğidir */

/* Bu, yazı boyutuna göre otomatik olarak ayarlanır */
```

### Bağlama Göre Ayarlamalar

| Bağlam | Karakter Aralığı |
|---------|-----------------|
| Masaüstü makale | 60-75 karakter |
| Mobil | 35-50 karakter |
| Yan panel metni | 30-45 karakter |
| Geniş monitörler | Yine de ~75ch ile sınırlandırın |

---

## 5. Duyarlı (Responsive) Tipografi Prensipleri

### Sorun Tanımı

```
Sabit boyutlar iyi ölçeklenmez:
├── Masaüstü boyutu mobilde çok büyük kalır
├── Mobil boyutu masaüstünde çok küçük kalır
└── Kesme noktası (breakpoint) sıçramaları rahatsız edici hissettirir
```

### Akışkan Tipografi (Fluid Typography - clamp)

```css
/* Sözdizimi: clamp(MİN, TERCİH EDİLEN, MAKS) */
font-size: clamp(
  MINIMUM_BOYUT,
  AKISKAN_HESAPLAMA,
  MAKSIMUM_BOYUT
);

/* AKISKAN_HESAPLAMA genellikle şöyledir: 
   temel + viewport-relative-unit */
```

### Ölçeklendirme Stratejisi

| Öğe | Ölçeklendirme Davranışı |
|---------|-----------------|
| Gövde metni | Hafif ölçeklendirme (1rem → 1.125rem) |
| Alt başlıklar | Orta düzeyde ölçeklendirme |
| Başlıklar | Daha dramatik ölçeklendirme |
| Display (Ekran) metni | En dramatik ölçeklendirme |

---

## 6. Ağırlık (Weight) ve Vurgu Prensipleri

### Semantik Ağırlık Kullanımı

| Ağırlık Aralığı | Adı | Kullanım Alanı |
|--------------|------|---------|
| 300-400 | Light/Normal | Gövde metni, paragraflar |
| 500 | Medium | Hafif vurgu |
| 600 | Semibold | Alt başlıklar, etiketler |
| 700 | Bold | Başlıklar, güçlü vurgu |
| 800-900 | Heavy/Black | Hero metni, büyük başlıklar |

### Kontrast Yaratma

```
İyi kontrast = en az 2 ağırlık seviyesi atlamak
├── 400 gövde + 700 başlık = İYİ
├── 400 gövde + 500 vurgu = HAFİF/ZAYIF
├── 600 başlık + 700 alt başlık = BİRBİRİNE ÇOK BENZER
```

### Kaçınılması Gerekenler

- ❌ Çok fazla farklı ağırlık kullanımı (sayfa başına maksimum 3-4)
- ❌ Hiyerarşi için birbirine çok yakın ağırlıklar (400/500)
- ❌ Uzun metinler için çok ağır/kalın fontlar

---

## 7. Harf Aralığı (Tracking)

### Prensipler

```
Büyük metin (başlıklar): Daha dar harf aralığı
├── Harfler büyüktür, boşluklar daha büyük hissedilir
└── Hafif negatif aralık daha iyi görünür

Küçük metin (gövde): Normal veya hafif geniş aralık
├── Küçük boyutlarda okunabilirliği artırır
└── Gövde metni için asla negatif aralık kullanmayın

HEPSİ BÜYÜK HARF: Her zaman daha geniş harf aralığı
├── Büyük harflerin alt/üst uzantıları yoktur
└── Doğru hissettirmesi için daha fazla alana ihtiyaç duyar
```

### Ayarlama Yönergeleri

| Bağlam | Harf Aralığı Ayarı |
|---------|---------------------|
| Display/Hero | -%2 ile -%4 arası |
| Başlıklar | -%1 ile -%2 arası |
| Gövde metni | %0 (normal) |
| Küçük metin | +%1 ile +%2 arası |
| HEPSİ BÜYÜK | +%5 ile +%10 arası |

---

## 8. Hiyerarşi Prensipleri

### Yazı Yoluyla Görsel Hiyerarşi

```
Hiyerarşi yaratma yolları:
├── BOYUT (en belirgin olan)
├── AĞIRLIK (kalın olan öne çıkar)
├── RENK (kontrast seviyeleri)
├── BOŞLUK (kenar boşlukları bölümleri ayırır)
└── KONUM (üstte olan önemlidir)
```

### Tipik Hiyerarşi Düzeni

| Seviye | Özellikler |
|-------|-----------------|
| Birincil (H1) | En büyük, en kalın, en belirgin |
| İkincil (H2) | Belirgin şekilde daha küçük ama hala kalın |
| Üçüncil (H3) | Orta boy, sadece ağırlık farkı kullanılabilir |
| Gövde | Standart boyut ve ağırlık |
| Altyazı/Meta | Daha küçük, genellikle daha açık renk |

### Hiyerarşiyi Test Etme

Sorun: "Bakışta neyin en önemli olduğunu anlayabiliyor muyum?"

Gözlerinizi kısarak sayfalara baktığınızda, hiyerarşi hala net olmalıdır.

---

## 9. Okunabilirlik Psikolojisi

### F-Tipi Okuma Deseni (F-Pattern)

```
Kullanıcılar F-şeklinde tarar:
├── Üst kısım boyunca (ilk satır)
├── Sol kenardan aşağıya doğru
├── Tekrar yatay (alt başlık)
└── Sol kenardan aşağı devam eder
```

**Sonuç**: Kritik bilgiler solda ve başlıklarda olmalıdır.

### Anlaşılabilirlik İçin Gruplandırma (Chunking)

- Kısa paragraflar (en fazla 3-4 satır)
- Net alt başlıklar
- Listeler için madde işaretleri
- Bölümler arasında beyaz boşluk (whitespace)

### Bilişsel Kolaylık

- Tanıdık yazı tipleri = Daha kolay okuma
- Yüksek kontrast = Daha az yorulma
- Tutarlı desenler = Tahmin edilebilir yapı

---

## 10. Tipografi Seçimi Kontrol Listesi

Tipografiyi kesinleştirmeden önce:

- [ ] **Kullanıcıya font tercihleri soruldu mu?**
- [ ] **Marka ve bağlama uygunluk değerlendirildi mi?**
- [ ] **Uygun ölçek oranı seçildi mi?**
- [ ] **2-3 font ailesi ile sınırlandırıldı mı?**
- [ ] **Tüm boyutlarda okunabilirlik test edildi mi?**
- [ ] **Satır genişliği kontrol edildi mi (45-75ch)?**
- [ ] **Erişilebilirlik için kontrast doğrulandı mı?**
- [ ] **Önceki projenizden farklı mı?**

### Anti-Desenler (Yapılmaması Gerekenler)

- ❌ Her projede aynı fontları kullanmak
- ❌ Çok fazla font ailesi kullanmak
- ❌ Stil uğruna okunabilirliği feda etmek
- ❌ Duyarlı (responsive) olmayan sabit boyutlar
- ❌ Gövde metni için dekoratif fontlar kullanmak

---

> **Unutmayın**: Tipografi, iletişimin netliği ile ilgilidir. Kişisel tercihlere göre değil, içerik ihtiyaçlarına ve hedef kitleye göre seçim yapın.
