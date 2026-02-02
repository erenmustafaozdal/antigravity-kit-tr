# Özellik Geliştirme (Feature Building)

> Yeni özelliklerin nasıl analiz edileceği ve uygulanacağı.

## Özellik Analizi

```
İstek: "ödeme sistemi ekle"

Analiz:
├── Gereken Değişiklikler:
│   ├── Veritabanı: orders (siparişler), payments (ödemeler) tabloları
│   ├── Backend: /api/checkout, /api/webhooks/stripe
│   ├── Frontend: CheckoutForm (Ödeme Formu), PaymentSuccess (Başarılı Ödeme Sayfası)
│   └── Yapılandırma: Stripe API anahtarları
│
├── Bağımlılıklar:
│   ├── stripe paketi
│   └── Mevcut kullanıcı kimlik doğrulaması (auth)
│
└── Tahmini Süre: 15-20 dakika
```

## Yinelemeli İyileştirme Süreci

```
1. Mevcut projeyi analiz et
2. Değişiklik planı oluştur
3. Planı kullanıcıya sun
4. Onay al
5. Değişiklikleri uygula
6. Test et
7. Önizlemeyi göster
```

## Hata Yönetimi

| Hata Türü | Çözüm Stratejisi |
|------------|-------------------|
| TypeScript Hatası | Tipi düzelt, eksik import'u ekle |
| Eksik Bağımlılık | npm install komutunu çalıştır |
| Port Çakışması | Alternatif port öner |
| Veritabanı Hatası | Migrasyonu kontrol et, bağlantıyı doğrula |

## Kurtarma Stratejisi (Recovery Strategy)

```
1. Hatayı tespit et
2. Otomatik düzeltmeyi dene
3. Başarısız olursa kullanıcıya bildir
4. Alternatif öner
5. Gerekiyorsa geri al (rollback)
```
