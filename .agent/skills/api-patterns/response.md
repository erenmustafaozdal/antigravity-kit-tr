# Yanıt Formatı (Response Format) Prensipleri

> İstikrar esastır - bir format seçin ve ona sadık kalın.

## Yaygın Desenler

```
Birini seçin:
├── Zarf (Envelope) deseni ({ success, data, error })
├── Doğrudan veri (sadece kaynağı dönderin)
├── HAL / JSON:API (hiper ortam desteği)
```

## Hata Yanıtları

```
Şunları dahil edin:
├── Hata kodu (programatik yönetim için)
├── Kullanıcı mesajı (ekranda göstermek için)
├── Detaylar (hata ayıklama ve alan bazlı hatalar için)
├── İstek ID'si (destek süreçleri için)
└── ASLA dahili sistem detaylarını dahil etmeyin (güvenlik!)
```

## Sayfalama (Pagination) Türleri

| Tür | En İyi Kullanım | Avantaj/Dezavantaj |
|------|----------|------------|
| **Offset** | Basit yapılar, sayfa atlama | Büyük veri setlerinde performans düşer |
| **Cursor** | Büyük veri setleri | Belirli bir sayfaya atlanamaz |
| **Keyset** | Performansın kritik olduğu yerler | Sıralanabilir anahtar gerektirir |

### Seçim Soruları

1. Veri seti ne kadar büyük?
2. Kullanıcıların belirli sayfalara atlaması gerekiyor mu?
3. Veriler çok sık değişiyor mu?
