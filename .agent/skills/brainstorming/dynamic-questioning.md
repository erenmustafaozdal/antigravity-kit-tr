# Dinamik Soru Üretimi (Dynamic Question Generation)

> **PRENSİP:** Sorular sadece veri toplamak için değil, **mimari sonuçları ortaya çıkarmak** içindir.
>
> Her soru; maliyeti, karmaşıklığı veya zaman çizelgesini etkileyen somut bir uygulama kararına bağlanmalıdır.

---

## 🧠 Temel Prensipler

### 1. Sorular Sonuçları Belirler

İyi bir soru "Hangi rengi istersiniz?" değil, şudur:

```markdown
❌ YANLIŞ: "Hangi kimlik doğrulama yöntemini istersiniz?"
✅ DOĞRU: "Kullanıcılar e-posta/şifre ile mi yoksa sosyal medya hesaplarıyla mı giriş yapmalı?

   Etki:
   - E-posta/Şifre → Şifre sıfırlama, hashleme, 2FA altyapısı gerekir
   - Sosyal Medya → OAuth sağlayıcıları, profil eşleştirme, daha az kontrol imkanı

   Takas (Trade-off): Güvenlik vs. Geliştirme süresi vs. Kullanıcı sürtünmesi"
```

### 2. İçerikten Önce Bağlam

Öncelikle bu isteğin **nereye** oturduğunu anlayın:

| Bağlam | Soru Odağı |
|---------|----------------|
| **Sıfırdan Proje** (Greenfield) | Temel kararlar: teknoloji yığını, barındırma, ölçek |
| **Özellik Ekleme** | Entegrasyon noktaları, mevcut desenler, kırılma riski olan yerler |
| **Refactor** | Neden refactor? Performans mı? Sürdürülebilirlik mi? Bozulan ne? |
| **Debug** | Belirtiler → Kök neden → Yeniden oluşturma yolu |

### 3. Minimum Gerekli Sorular

**PRENSİP:** Her soru, uygulama yolundaki bir ayrımı ortadan kaldırmalıdır.

```
Soru Öncesi:
├── Yol A: X Yap (5 dk)
├── Yol B: Y Yap (15 dk)
└── Yol C: Z Yap (1 saat)

Soru Sonrası:
└── Onaylanan Yol: X Yap (5 dk)
```

Bir soru uygulama yollarını azaltmıyorsa → **SİLEBİLİRSİNİZ**.

### 4. Sorular Varsayım Değil, Veri Üretir

```markdown
❌ VARSAYIM: "Kullanıcı muhtemelen ödemeler için Stripe ister"
✅ SORU: "İhtiyaçlarınıza hangi ödeme sağlayıcısı daha uygun?

   Stripe → En iyi dokümantasyon, %2.9 + $0.30, ABD merkezli
   LemonSqueezy → Kayıtlı Satıcı (MoR), %5 + $0.50, küresel vergiler
   Paddle → Karmaşık fiyatlandırma, AB KDV yönetiminde iyi, kurumsal odaklı"
```

---

## 📋 Soru Üretme Algoritması

```
GİRDİ: Kullanıcı isteği + Bağlam (yeni proje/özellik/refactor/debug)
│
├── ADIM 1: İsteği Çözümle
│   ├── Alanı çıkar (e-ticaret, auth, real-time, cms vb.)
│   ├── Özellikleri çıkar (açıkça belirtilen ve ima edilen)
│   └── Ölçek göstergelerini çıkar (kullanıcı sayısı, veri hacmi, sıklık)
│
├── ADIM 2: Karar Noktalarını Belirle
│   ├── Kodlamadan önce ne karar VERİLMELİ? (engelleyici)
│   ├── Ne daha sonra kararlaştırılabilir? (ertelenebilir)
│   └── Nelerin MİMARİ etkisi var? (yüksek kaldıraçlı)
│
├── ADIM 3: Soruları Üret (Öncelik Sırası)
│   ├── P0: Engelleyici kararlar (cevaplanmadan ilerlenemez)
│   ├── P1: Yüksek kaldıraçlı (uygulamanın %30'undan fazlasını etkiler)
│   ├── P2: Orta kaldıraçlı (belirli özellikleri etkiler)
│   └── P3: Olsa iyi olur (uç durumlar, optimizasyon)
│
└── ADIM 4: Her Soruyu Formatla
    ├── Ne: Net soru cümlesi
    ├── Neden: Uygulama üzerindeki etkisi
    ├── Seçenekler: Takaslar (sadece A vs B değil)
    └── Varsayılan: Kullanıcı cevaplamazsa ne olur
```

---

## 🎯 Alan Bazlı Soru Bankaları

### E-Ticaret

| Soru | Neden Önemli? | Takaslar (Trade-offs) |
|----------|----------------|------------|
| **Tekli mi Çoklu Satıcı mı?** | Çoklu satıcı → Komisyon mantığı, satıcı panelleri, ödeme dağıtımı | +Gelir, -Karmaşıklık |
| **Stok Takibi Yapılacak mı?** | Stok tabloları, rezervasyon mantığı, düşük stok uyarıları gerekir | +Hassasiyet, -Geliştirme süresi |
| **Dijital mi Fiziksel Ürün mü?** | Dijital → İndirme linkleri, kargo yok | Fiziksel → Kargo API'leri, takip |
| **Abonelik mi Tek Seferlik mi?** | Abonelik → Düzenli faturalandırma, yapılandırma | +Gelir, -Karmaşıklık |

### Kimlik Doğrulama (Authentication)

| Soru | Neden Önemli? | Takaslar (Trade-offs) |
|----------|----------------|------------|
| **Sosyal Giriş Lazım mı?** | OAuth sağlayıcıları vs. şifre sıfırlama altyapısı | +Kullanıcı Deneyimi, -Kontrol |
| **Rol Bazlı İzinler?** | RBAC tabloları, yetki kontrolü, admin paneli | +Güvenlik, -Geliştirme süresi |
| **2FA Gerekiyor mu?** | TOTP/SMS altyapısı, yedek kodlar, kurtarma akışı | +Güvenlik, -Kullanıcı sürtünmesi |
| **E-posta Doğrulama?** | Doğrulama tokenları, e-posta servisi, tekrar gönderme mantığı | +Güvenlik, -Kayıt olma sürtünmesi |

### Gerçek Zamanlı (Real-time)

| Soru | Neden Önemli? | Takaslar (Trade-offs) |
|----------|----------------|------------|
| **WebSocket mi Polling mi?** | WS → Sunucu ölçeklendirme, bağlantı yönetimi | Polling → Daha basit, daha yüksek gecikme |
| **Beklenen Eşzamanlı Kullanıcı?** | <100 → Tek sunucu, >1000 → Redis pub/sub, >10k → özel altyapı | +Ölçek, -Karmaşıklık |
| **Mesaj Kalıcılığı?** | Geçmiş mesaj tabloları, depolama maliyeti, sayfalama | +Kullanıcı Deneyimi, -Depolama |
| **Uçucu mu Kalıcı mı?** | Uçucu → Bellek içi, Kalıcı → Veritabanına yazdıktan sonra yayma | +Güvenilirlik, -Gecikme |

---

## 📐 Dinamik Soru Şablonu

```markdown
[ALAN] [ÖZELLİK] isteğinize dayanarak:

## 🔴 KRİTİK (Engelleyici Kararlar)

### 1. **[KARAR NOKTASI]**

**Soru:** [Net ve spesifik soru cümlesi]

**Bu Neden Önemli:**
- [Mimari sonucu açıklayın]
- [Etkilediği alanlar: maliyet / karmaşıklık / zaman çizelgesi / ölçek]

**Seçenekler:**
| Seçenek | Artılar | Eksiler | En Uygun Durum |
|--------|------|------|----------|
| A | [Avantaj] | [Dezavantaj] | [Senaryo] |
| B | [Avantaj] | [Dezavantaj] | [Senaryo] |

**Belirtilmezse:** [Varsayılan seçim + gerekçesi]

---

## 🟡 YÜKSEK KALDIRAÇLI (Uygulamayı Etkileyenler)

### 2. **[KARAR NOKTASI]**
[Aynı format]

---

## 🟢 OLSA İYİ OLUR (Uç Durumlar)

### 3. **[KARAR NOKTASI]**
[Aynı format]
```

---

## 🔄 Yinelemeli Sorgulama

### İlk Aşama (3-5 Soru)
**Engelleyici kararlara** odaklanın. Cevap almadan ilerlemeyin.

### İkinci Aşama (Uygulama Başladıktan Sonra)
Desenler ortaya çıktıkça:
- "Bu özellik [X] gerektiriyor. [Uç durumu] şimdi mi yönetelim yoksa erteleyelim mi?"
- "[A Deseni]'ni kullanıyoruz. [B Özelliği] de aynı deseni mi takip etmeli?"

### Üçüncü Aşama (Optimizasyon)
İşlevsellik çalıştığında:
- "[X] noktasında performans darboğazı var. Şimdi mi optimize edelim yoksa şimdilik yeterli mi?"
- "[Y] yapısını sürdürülebilirlik için refactor edelim mi yoksa olduğu gibi mi bırakalım?"

---

## 🎭 Örnek: Tam Soru Üretimi

```
KULLANICI İSTEĞİ: "Bir Instagram klonu yap"

ADIM 1: Çözümle
├── Alan: Sosyal Medya
├── Özellikler: Fotoğraf paylaşımı, etkileşim (beğeni/yorum), profil sayfaları
├── İma Edilen: Akış (feed), takip etme, kimlik doğrulama
└── Ölçek: Potansiyel olarak yüksek (sosyal uygulamalar hızla yayılabilir)

ADIM 2: Karar Noktaları
├── Engelleyici: Depolama stratejisi, auth yöntemi, akış türü
├── Yüksek Kaldıraçlı: Gerçek zamanlı bildirimler, veri modeli karmaşıklığı
└── Ertelenebilir: Analitik, gelişmiş arama, reels/video özellikleri

ADIM 3: Soruları Üret (Öncelik)

P0 (Engelleyici):
1. Depolama Stratejisi → Mimariyi, maliyeti ve hızı etkiler
2. Akış Algoritması → Veritabanı sorgularını ve karmaşıklığı etkiler
3. Auth Yöntemi → Geliştirme süresini, UX'i ve güvenliği etkiler

P1 (Yüksek Kaldıraçlı):
4. Gerçek Zamanlı Bildirimler → WebSocket vs polling
5. Medya İşleme → İstemci tarafı vs sunucu tarafı optimizasyon

P2 (Ertelenebilir):
6. Hikaye/Reels → Önemli bir kapsam genişlemesi (scope creep), v2'ye ertele
7. DM/Chat → Ayrı bir alt sistem, v2'ye ertele

ADIM 4: Çıktıyı Formatla
```

---

## 📊 Üretilen Çıktı (Örnek)

```
Instagram klonu isteğinize dayanarak:

## 🔴 KRİTİK KARARLAR (Cevaplanmadan İlerlenemez)

### 1. **Fotoğraf Depolama Stratejisi**

**Soru:** Kullanıcı fotoğrafları nerede saklanacak ve servis edilecek?

**Bu Neden Önemli:**
- Etkileri: Aylık barındırma maliyetleri, sayfa yükleme hızı, CDN karmaşıklığı
- Yüksek hacimli sosyal uygulamalar: 1000 kullanıcı × 10 fotoğraf × 2MB = 20GB depolama

**Seçenekler:**
| Seçenek | Maliyet | Hız | Karmaşıklık | En Uygun Durum |
|--------|------|-------|------------|----------|
| **Cloudinary** | $89/ay (25GB) | Hızlı (CDN) | Düşük | MVP, hızlı çıkış |
| **AWS S3 + CloudFront** | $0.023/GB | Hızlı (CDN) | Orta | Prodüksiyon, maliyet odaklı |
| **Supabase Storage** | Ücretsiz 1GB | Orta | Düşük | Küçük ölçek, basit yapı |
| **Yerel Depolama** | Sunucu bedeli | Yavaş | Düşük | Sadece geliştirme aşaması |

**Belirtilmezse:** Cloudinary (MVP için dengeli seçim)

---

### 2. **Akış (Feed) Algoritması Seçimi**

**Soru:** Ana akış nasıl çalışmalı?

**Bu Neden Önemli:**
- Etkileri: Veritabanı sorgu karmaşıklığı, önbellekleme stratejisi, geliştirme süresi
- Algoritmik akışlar ML altyapısı ve sıralama sinyalleri gerektirir

**Seçenekler:**
| Seçenek | Karmaşıklık | Veritabanı Etkisi | En Uygun Durum |
|--------|------------|-----------------|----------|
| **Kronolojik** | Düşük | Basit sorgu | Erken aşama, şeffaflık |
| **Sadece Takip Edilenler** | Orta | Pagination + JOIN | Çoğu sosyal uygulama |
| **Algoritmik** | Yüksek | Önceden hesaplanmış tablolar | Instagram rakibi projeler |

**Belirtilmezse:** Sadece Takip Edilenler (Sosyal uygulama için dengeli seçim)

---

### 3. **Kimlik Doğrulama (Auth) Yaklaşımı**

**Soru:** Kullanıcılar nasıl kayıt olacak ve giriş yapacak?

**Bu Neden Önemli:**
- Etkileri: Geliştirme süresi (2-5 saat), güvenlik duruşu, kullanıcı deneyimi

**Seçenekler:**
| Seçenek | Geliştirme Süresi | Güvenlik | Deneyim | En Uygun Durum |
|--------|----------|----------|-----|----------|
| **E-posta/Şifre** | 4-5 saat | Yüksek (2FA varsa) | Orta | Tam kontrol gerekliyse |
| **Sadece Sosyal** | 1-2 saat | Sağlayıcıya bağlı | Akıcı | B2C, hızlı çıkış |
| **Magic Link** | 2-3 saat | Orta | Çok akıcı | Güvenlik odaklı |
| **Clerk/Auth0** | 1 saat | Yüksek | Akıcı | En hızlı piyasaya çıkış |

**Belirtilmezse:** Clerk (MVP için en hızlısı)

---

## 🟡 YÜKSEK KALDIRAÇLI (Mimariyi Etkileyenler)

### 4. **Gerçek Zamanlı Bildirimler**

**Soru:** Kullanıcıların beğeni/yorumlar için anlık bildirimlere ihtiyacı var mı?

**Bu Neden Önemli:**
- WebSocket altyapı karmaşıklığı ekler (ölçeklenme için Redis pub/sub vb.)
- Polling daha basittir ancak gecikmesi daha yüksektir

**Seçenekler:**
| Seçenek | Karmaşıklık | Ölçek Maliyeti | En Uygun Durum |
|--------|------------|------------|----------|
| **WebSocket + Redis** | Yüksek | $10+/ay | >1000 eşzamanlı kullanıcı |
| **Polling (30sn)** | Düşük | DB sorguları | <1000 kullanıcı |
| **Gerçek Zamanlı Yok** | Yok | Yok | MVP, önce doğrula |

**Belirtilmezse:** MVP için Polling (WebSocket'i doğrulamadan sonra ekle)

---

## 🟢 OLSA İYİ OLUR (v2'ye Ertele)

### 5. **Video/Reels Desteği**
- Büyük karmaşıklık (video işleme, yayılım altyapısı)
- Öneri: Sadece fotoğraf ile başlayın, videoyu doğrulamadan sonra ekleyin.

### 6. **Doğrudan Mesajlaşma (DM)**
- Ayrı bir alt sistem (chat altyapısı akıştan farklıdır)
- Öneri: Gerçek zamanlı için Pusher/Stream kullanın veya tamamen erteleyin.

---

## 📋 Özet Tablo

| Karar | Öneri | Değişirse Ne Olur? |
|----------|----------------|------------|
| Depolama | Cloudinary | +3 saat kurulum |
| Akış | Sadece Takipçiler | +2 saat sorgu optimizasyonu |
| Auth | Clerk | -3 saat geliştirme süresi |
| Gerçek Zamanlı | Polling | +5 saat WebSocket kurulumu |
| Video | v2'ye ertele | N/A |
| DM | v2'ye ertele | N/A |

**Tahmini Toplam MVP Süresi:** Yukarıdaki önerilerle 15-20 saat
```

---

## 🎯 Prensiplerin Özeti

1. **Her soru = Bir mimari karar** → Sadece veri toplama değil.
2. **Takasları göster** → Kullanıcı sonuçları anlasın.
3. **Engelleyici kararları önceliklendir** → Onlar olmadan ilerlenemez.
4. **Varsayılanlar sunun** → Kullanıcı cevap vermezse bile ilerleyebilelim.
5. **Alana duyarlı olun** → E-ticaret soruları ≠ Auth soruları ≠ Real-time soruları.
6. **Yinelemeli ilerleyin** → Uygulama sırasında desenler netleştikçe daha fazla soru sorun.
