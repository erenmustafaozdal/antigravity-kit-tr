# İstek Sınırlama (Rate Limiting) Prensipleri

> API'nizi suiistimallere ve aşırı yüklenmeye karşı koruyun.

## Neden İstek Sınırlama Yapılmalı?

```
Şunlara karşı koruma sağlayın:
├── Kaba kuvvet (Brute force) saldırıları
├── Kaynak tükenmesi (Resource exhaustion)
├── Beklenmedik maliyet aşımları (kullandıkça öde ise)
└── Haksız veya dengesiz kullanım
```

## Strateji Seçimi

| Tür | Nasıl Çalışır | Ne Zaman Kullanılır |
|------|-----|------|
| **Token bucket** | Anlık yüklenmeye (burst) izin verir, zamanla dolar | Çoğu API için |
| **Sliding window**| Pürüzsüz bir dağılım sağlar | Katı limitler gerektiğinde |
| **Fixed window** | Her pencere için basit sayaçlar tutar | Basit ihtiyaçlar için |

## Yanıt Header Bilgileri

```
Header'lara şunları dahil edin:
├── X-RateLimit-Limit (maksimum istek sayısı)
├── X-RateLimit-Remaining (kalan istek hakkı)
├── X-RateLimit-Reset (limitin ne zaman sıfırlanacağı)
└── Limit aşıldığında 429 durum kodunu döndürün
```
