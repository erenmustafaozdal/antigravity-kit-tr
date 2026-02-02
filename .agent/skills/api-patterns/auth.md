# Kimlik Doğrulama Desenleri (Authentication Patterns)

> Kullanım durumuna göre kimlik doğrulama deseni seçimi.

## Seçim Rehberi

| Desen | En İyi Kullanım |
|---------|----------|
| **JWT** | Durumsuz (Stateless) yapılar, mikro servisler |
| **Oturum (Session)** | Geleneksel web uygulamaları, basit yapılar |
| **OAuth 2.0** | Üçüncü taraf entegrasyonları |
| **API Anahtarları** | Sunucudan sunucuya iletişim, herkese açık API'ler |
| **Passkey** | Modern şifresiz doğrulama (2025+) |

## JWT Prensipleri

```
Önemli Kurallar:
├── İmzayı HER ZAMAN doğrulayın
├── Son kullanma tarihini (expiration) kontrol edin
├── Sadece gerekli verileri (claims) dahil edin
├── Kısa süreli erişim tokenı + yenileme (refresh) tokenı kullanın
└── JWT içinde ASLA hassas veri saklamayın
```
