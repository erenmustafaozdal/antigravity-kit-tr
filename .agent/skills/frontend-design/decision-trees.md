# Karar Ağaçları ve Bağlam Şablonları

> Sabit çözümlere değil, bağlam temelli tasarım DÜŞÜNCESİNE odaklanır.
> **Bunlar karar verme REHBERLERİDİR, kopyala-yapıştır şablonları değildir.**
> **UX psikolojisi prensipleri (Hick, Fitts vb.) için bakınız:** [ux-psychology.md](ux-psychology.md)

---

## ⚠️ Bu Dosya Nasıl Kullanılır?

Bu dosya kopyalamanıza değil, KARAR VERMENİZE yardımcı olur.

- Karar Ağaçları → Seçenekler üzerinde DÜŞÜNMEnize yardımcı olur
- Şablonlar → Kesin değerleri değil, YAPI ve PRENSİPLERİ gösterir
- Uygulamadan önce **her zaman kullanıcı tercihlerini sorun**
- Hex kodlarını kopyalamayın, bağlama göre **sıfırdan paletler üretin**
- Kararları doğrulamak için ux-psychology.md dosyasındaki **UX yasalarını uygulayın**

---

## 1. Ana Karar Ağacı

```
┌─────────────────────────────────────────────────────────────┐
│                       NE İNŞA EDİYORSUNUZ?                  │
└─────────────────────────────────────────────────────────────┘
                               │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
   E-TİCARET             SaaS/UYGULAMA         İÇERİK
   - Ürün sayfaları      - Dashboard           - Blog
   - Ödeme (Checkout)    - Araçlar             - Portfolyo
   - Katalog             - Admin paneli        - Açılış sayfası
        │                     │                     │
        ▼                     ▼                     ▼
   PRENSİPLER:           PRENSİPLER:           PRENSİPLER:
   - Güven               - Fonksiyonellik      - Hikaye Anlatımı
   - Eylem               - Netlik              - Duygu
   - Aciliyet            - Verimlilik          - Yaratıcılık
```

---

## 2. Hedef Kitle Karar Ağacı

### Hedef kullanıcınız kim?

```
HEDEF KİTLE
      │
      ├── Z Kuşağı (18-25)
      │   ├── Renkler: Cesur, canlı, beklenmedik kombinasyonlar
      │   ├── Yazı: Büyük, dışavurumcu, değişken
      │   ├── Düzen: Mobil öncelikli, dikey, hızlı tüketilebilir
      │   ├── Efektler: Hareketli, oyunlaştırma, etkileşimli
      │   └── Yaklaşım: Otantik, hızlı, kurumsallıktan uzak
      │
      ├── Y Kuşağı (26-41)
      │   ├── Renkler: Mat, toprak tonları, sofistike
      │   ├── Yazı: Temiz, okunaklı, fonksiyonel
      │   ├── Düzen: Responsive, kart tabanlı, organize
      │   ├── Efektler: Hafif, sadece amaca hizmet eden
      │   └── Yaklaşım: Değer odaklı, şeffaf, sürdürülebilir
      │
      ├── X Kuşağı (42-57)
      │   ├── Renkler: Profesyonel, güven veren, muhafazakar
      │   ├── Yazı: Tanıdık, net, ciddi
      │   ├── Düzen: Geleneksel hiyerarşi, tahmin edilebilir
      │   ├── Efektler: Minimal, fonksiyonel geri bildirim
      │   └── Yaklaşım: Doğrudan, verimli, güvenilir
      │
      ├── Baby Boomer'lar (58+)
      │   ├── Renkler: Yüksek kontrastlı, basit, net
      │   ├── Yazı: Büyük boyutlar, yüksek okunabilirlik
      │   ├── Düzen: Basit, doğrusal, karmaşadan uzak
      │   ├── Efektler: Yok veya çok minimal
      │   └── Yaklaşım: Net, detaylı, güvenilir
      │
      └── B2B / Kurumsal
          ├── Renkler: Profesyonel palet, mat tonlar
          ├── Yazı: Temiz, veri dostu, taranabilir
          ├── Düzen: Izgara tabanlı, organize, verimli
          ├── Efektler: Profesyonel, hafif
          └── Yaklaşım: Uzmanlık ve çözüm odaklı, ROI (yatırım getirisi) odaklı
```

---

## 3. Renk Seçimi Karar Ağacı

### Sabit hex kodları yerine şu süreci izleyin:

```
HANGİ DUYGUYU / EYLEMİ İSTİYORSUNUZ?
             │
             ├── Güven ve Güvenlik
             │   └── Düşünün: Mavi ailesi, profesyonel nötrler
             │       → Kullanıcıya spesifik ton tercihini SORUN
             │
             ├── Büyüme ve Sağlık
             │   └── Düşünün: Yeşil ailesi, doğal tonlar
             │       → Eko/doğa/zindelik odağı olup olmadığını SORUN
             │
             ├── Aciliyet ve Eylem
             │   └── Düşünün: VURGU (ACCENT) olarak sıcak renkler (turuncu/kırmızı)
             │       → İdareli kullanın, uygunluğunu SORUN
             │
             ├── Lüks ve Premium
             │   └── Düşünün: Derin koyu renkler, metalikler, ölçülü paletler
             │       → Marka konumlandırmasını SORUN
             │
             ├── Yaratıcı ve Oyunbaz
             │   └── Düşünün: Çok renkli, beklenmedik kombinasyonlar
             │       → Marka kişiliğini SORUN
             │
             └── Sakin ve Minimal
                 └── Düşünün: Tek vurgu rengiyle nötr tonlar
                     → Markaya hangi vurgu renginin uyacağını SORUN
```

### Süreç:
1. Gerekli duyguyu belirleyin
2. Renk AİLESİNE indirin
3. Aile içindeki tercih için kullanıcıya SORUN
4. HSL prensiplerini kullanarak sıfırdan palet üretin

---

## 4. Tipografi Karar Ağacı

```
İÇERİK TÜRÜ NEDİR?
          │
          ├── Veri Yoğunluklu (Dashboard, SaaS)
          │   ├── Stil: Sans-serif, net, kompakt
          │   ├── Ölçek: Daha dar oranlar (1.125-1.2)
          │   └── Öncelik: Taranabilirlik, içerik yoğunluğu
          │
          ├── Editöryel (Blog, Dergi)
          │   ├── Stil: Serif başlık + Sans gövde metni iyi çalışır
          │   ├── Ölçek: Daha dramatik (1.333+)
          │   └── Öncelik: Okuma konforu, hiyerarşi
          │
          ├── Modern Teknoloji (Startup, SaaS Pazarlama)
          │   ├── Stil: Geometrik veya humanist sans
          │   ├── Ölçek: Dengeli (1.25)
          │   └── Öncelik: Modern his, netlik
          │
          ├── Lüks (Moda, Premium Ürün)
          │   ├── Stil: Zarif serif veya ince sans
          │   ├── Ölçek: Dramatik (1.5-1.618)
          │   └── Öncelik: Sofistike görünüm, geniş beyaz alanlar
          │
          └── Oyunbaz (Çocuklar, Oyunlar, Sosyal)
              ├── Stil: Yuvarlak hatlı, sıcak yazı tipleri
              ├── Ölçek: Değişken, dışavurumcu
              └── Öncelik: Eğlence, cana yakınlık, okunabilirlik
```

### Seçim Süreci:
1. İçerik türünü belirleyin
2. Stil YÖNÜNÜ seçin
3. Kullanıcının marka fontları olup olmadığını SORUN
4. Belirlenen yöne uygun yazı tiplerini seçin

---

## 5. E-Ticaret Yönergeleri {#e-commerce}

### Temel Prensipler (Sabit Kurallar Değil)
- **Önce Güven:** Güvenliği nasıl göstereceksiniz?
- **Eylem Odaklı:** CTA'ler (eylem düğmeleri) nerede?
- **Taranabilir:** Kullanıcılar ürünleri hızlıca karşılaştırabiliyor mu?

### Renk Yaklaşımı:
```
E-Ticaret genellikle şunlara ihtiyaç duyar:
├── Güven rengi (genellikle mavi ailesi) → Tercihi SORUN
├── Temiz arka plan (beyaz/nötr) → Markaya göre değişir
├── Eylem vurgusu (CTA'ler, indirimler için) → Aciliyet seviyesine göre
├── Başarı/hata semantikleri → Standart kurallar geçerlidir
└── Marka entegrasyonu → Mevcut renkleri SORUN
```

### Düzen (Layout) Prensipleri:
```
┌────────────────────────────────────────────────────┐
│  HEADER: Marka + Arama + Sepet                      │
│  (Kritik eylemleri görünür tutun)                   │
├────────────────────────────────────────────────────┤
│  GÜVEN BÖLGESİ: Neden bu siteye güvenilmeli?        │
│  (Kargo, iade, güvenlik - geçerliyse)               │
├────────────────────────────────────────────────────┤
│  HERO: Ana mesaj veya kampanya                      │
│  (Net CTA, tek odak noktası)                        │
├────────────────────────────────────────────────────┤
│  KATEGORİLER: Kolay navigasyon                      │
│  (Görsel, filtrelenebilir, taranabilir)             │
├────────────────────────────────────────────────────┤
│  ÜRÜNLER: Kolay karşılaştırma                       │
│  (Fiyat, puan, hızlı işlemler görünür olmalı)       │
├────────────────────────────────────────────────────┤
│  SOSYAL KANIT: Diğerleri neden güveniyor?           │
│  (Yorumlar, referanslar - mevcutsa)                 │
├────────────────────────────────────────────────────┤
│  FOOTER: Tüm dökümantasyon ve detaylar              │
│  (Politikalar, iletişim, güven damgaları)           │
└────────────────────────────────────────────────────┘
```

### Uygulanacak Psikoloji:
- Hick Yasası: Navigasyon seçeneklerini sınırlayın
- Fitts Yasası: CTA'leri uygun boyutta yapın
- Sosyal Kanıt: İlgili her yerde gösterin
- Kıtlık (Scarcity): Varsa dürüstçe kullanın

---

## 6. SaaS Dashboard Yönergeleri {#saas}

### Temel Prensipler
- **Önce Fonksiyonellik:** Süslemeden önce veri netliği
- **Sakin Arayüz (Calm UI):** Bilişsel yükü azaltın
- **Tutarlılık:** Tahmin edilebilir desenler

### Renk Yaklaşımı:
```
Dashboard genellikle şunlara ihtiyaç duyar:
├── Arka plan: Açık VEYA koyu (Tercihi SORUN)
├── Yüzey (Surface): Arka plandan hafif kontrastla ayrılmış
├── Birincil vurgu: Ana eylemler için
├── Veri renkleri: Başarı/uyarı/tehlike semantikleri
└── Mat renkler: İkincil bilgiler için
```

### Düzen (Layout) Prensipleri:
```
Şu desenleri değerlendirin (zorunlu değil):

SEÇENEK A: Kenar Çubuğu (Sidebar) + İçerik
├── Navigasyon için sabit yan panel
└── İçerik için ana alan

SEÇENEK B: Üst Menü (Top nav) + İçerik
├── Yatay navigasyon
└── Daha geniş yatay içerik alanı

SEÇENEK C: Daraltılabilir + Genişletilebilir
├── Sadece ikonlu kenar çubuğu genişler
└── Maksimum içerik alanı

→ Kullanıcının navigasyon tercihini SORUN
```

### Uygulanacak Psikoloji:
- Hick Yasası: Navigasyon öğelerini gruplandırın
- Miller Yasası: Bilgiyi parçalara bölün (chunking)
- Bilişsel Yük: Boşluk ve tutarlılıkla yönetin

---

## 7. Açılış Sayfası (Landing Page) Yönergeleri {#landing-page}

### Temel Prensipler
- **Hero Odaklı:** İlk izlenim en önemlisidir
- **Tek Odak:** Bir ana eylem düğmesi (CTA)
- **Duygusal:** Satıştan önce bağ kurun

### Renk Yaklaşımı:
```
Açılış sayfası genellikle şunlara ihtiyaç duyar:
├── Marka birincil rengi: Hero arka planı veya vurgusu
├── Temiz ikincil renk: Sayfanın çoğu için
├── CTA rengi: Her şeyden öne çıkmalı
├── Destekleyici: Bölümler, referanslar için
└── ÖNCE marka renklerini SORUN!
```

### Yapı Prensipleri:
```
┌────────────────────────────────────────────────────┐
│  Navigasyon: Minimal, CTA görünür                   │
├────────────────────────────────────────────────────┤
│  HERO: Yakala (Hook) + Değer + CTA                  │
│  (En önemli bölüm, en büyük etki)                   │
├────────────────────────────────────────────────────┤
│  SORUN: Kullanıcı ne tür bir acı/ihtiyaç çekiyor?    │
├────────────────────────────────────────────────────┤
│  ÇÖZÜM: Bunu nasıl çözüyorsunuz?                    │
├────────────────────────────────────────────────────┤
│  KANIT: Size neden inanmalılar?                     │
│  (Referanslar, logolar, istatistikler)              │
├────────────────────────────────────────────────────┤
│  NASIL: Sürecin basit açıklaması                    │
├────────────────────────────────────────────────────┤
│  FİYATLANDIRMA: Geçerliyse                           │
├────────────────────────────────────────────────────┤
│  SSS: İtirazları ve soruları adresleyin             │
├────────────────────────────────────────────────────┤
│  SON CTA: Ana eylemi tekrarlayın                    │
└────────────────────────────────────────────────────┘
```

### Uygulanacak Psikoloji:
- Viseral: Etkileyici bir hero izlenimi
- Seri Konum: Kritik bilgileri başa ve sona koyun
- Sosyal Kanıt: Referansları etkin kullanın

---

## 8. Portfolyo Yönergeleri {#portfolio}

### Temel Prensipler
- **Kişilik:** Kim olduğunuzu gösterin
- **İş Odaklı:** Bırakın projeler konuşsun
- **Akılda Kalıcı:** Şablonlardan sıyrılın

### Renk Yaklaşımı:
```
Portfolyo kişiseldir - birçok seçenek vardır:
├── Minimal: Nötrler + tek bir imza vurgu rengi
├── Cesur: Beklenmedik renk tercihleri
├── Karanlık: Melankolik, sanatsal his
├── Açık: Temiz, profesyonel his
└── Kişisel marka kimliğini SORUN!
```

### Yapı Prensipleri:
```
┌────────────────────────────────────────────────────┐
│  Navigasyon: Kişiliğinize özgü                       │
├────────────────────────────────────────────────────┤
│  GİRİŞ: Kimsiniz, ne yaparsınız?                    │
│  (Sıradan değil, akılda kalıcı yapın)               │
├────────────────────────────────────────────────────┤
│  İŞLER: Öne çıkan projeler                          │
│  (Büyük, görsel, etkileşimli)                       │
├────────────────────────────────────────────────────┤
│  HAKKINDA: Kişisel hikaye                           │
│  (Bağ kurmayı sağlar)                               │
├────────────────────────────────────────────────────┤
│  İLETİŞİM: Kolay ulaşılabilirlik                    │
│  (Net, doğrudan)                                    │
└────────────────────────────────────────────────────┘
```

### Uygulanacak Psikoloji:
- Von Restorff: Benzersiz şekilde akılda kalıcı olun
- Reflektif: Kişisel hikaye bağ kurmayı güçlendirir
- Duygusal: Profesyonellikten önce kişiliği yansıtın

---

## 9. Tasarım Öncesi Kontrol Listeleri

### HERHANGİ bir tasarıma başlamadan önce

- [ ] **Hedef kitle tanımlandı mı?** (tam olarak kim)
- [ ] **Ana hedef belirlendi mi?** (hangi eylem)
- [ ] **Kısıtlar biliniyor mu?** (zaman, marka, teknoloji)
- [ ] **İçerik mevcut mu?** (veya yer tutucu mu gerekiyor)
- [ ] **Kullanıcı tercihleri soruldu mu?** (renk, stil, düzen)

### Renk Seçmeden Önce

- [ ] **Kullanıcı tercihi soruldu mu?**
- [ ] **Bağlam değerlendirildi mi?** (sektör, duygu)
- [ ] **Varsayılan tercihlerinizin dışında mı?**
- [ ] **Erişilebilirlik kontrol edildi mi?**

### Düzeni (Layout) Kesinleştirmeden Önce

- [ ] **Hiyerarşi net mi?**
- [ ] **Ana CTA belirgin mi?**
- [ ] **Mobil/küçük ekranlar hesaba katıldı mı?**
- [ ] **İçerik yapıya uyuyor mu?**

### Teslim Etmeden Önce

- [ ] **Premium görünüyor mu (sıradan değil mi)?**
- [ ] **Bununla gurur duyar mıydınız?**
- [ ] **Son projenizden farklı mı?**

---

## 10. Karmaşıklık Tahmini

### Hızlı Projeler (Saatlik)
```
Basit açılış sayfası
Küçük portfolyo siteleri
Temel formlar
Tek bir bileşen tasarımı
```
→ Yaklaşım: Hızlı kararlar, odaklanmış uygulama

### Orta Ölçekli Projeler (Günlük)
```
Çok sayfalı web siteleri
Modülleri olan dashboard'lar
E-ticaret kategori sayfaları
Karmaşık form akışları
```
→ Yaklaşım: Token'ları belirleme, özel bileşen inşa etme

### Büyük Ölçekli Projeler (Haftalık)
```
Tam kapsamlı SaaS uygulaması
E-ticaret platformu
Özel tasarım sistemi (design system) inşa etme
Karmaşık iş akışları
```
→ Yaklaşım: Tam kapsamlı tasarım sistemi, dökümantasyon, testler

---

> **Unutmayın**: Bu şablonlar YAPIYI ve DÜŞÜNCE sürecini gösterir. Her projenin kendi benzersiz bağlamına göre taze renk, tipografi ve stil kararlarına ihtiyacı vardır. Belirsiz durumlarda SORUN.
