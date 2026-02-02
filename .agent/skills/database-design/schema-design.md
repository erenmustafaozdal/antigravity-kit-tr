# Şema Tasarım Prensipleri

> Normalizasyon, birincil anahtarlar (PK), zaman damgaları, ilişkiler.

## Normalizasyon Kararı

```
Ne zaman normalize edilmeli (tabloları ayır):
├── Veri satırlar arasında tekrarlanıyorsa
├── Güncelleme işlemi birden fazla yerin değişmesini gerektiriyorsa
├── İlişkiler netse
└── Sorgu desenleri bundan fayda sağlıyorsa

Ne zaman denormalize edilmeli (gömülü/kopya veri):
├── Okuma performansı kritikse
├── Veri nadiren değişiyorsa
├── Veri her zaman birlikte çekiliyorsa
└── Daha basit sorgular gerekiyorsa
```

## Birincil Anahtar (Primary Key) Seçimi

| Tür | Ne Zaman Kullanılır |
|------|----------|
| **UUID** | Dağıtık sistemler, güvenlik |
| **ULID** | UUID + zamana göre sıralanabilir |
| **Auto-increment** | Basit uygulamalar, tek veritabanı |
| **Doğal Anahtar** | Çok nadiren (iş mantığı taşıyan anahtarlar) |

## Zaman Damgası (Timestamp) Stratejisi

```
Her tablo için:
├── created_at → Oluşturulma zamanı
├── updated_at → Son güncelleme zamanı
└── deleted_at → Yazılımsal silme (soft delete - gerekliyse)

TIMESTAMP yerine TIMESTAMPTZ (zaman dilimi ile birlikte) kullanın.
```

## İlişki Türleri

| Tür | Durum | Uygulama |
|------|------|----------------|
| **Bire-Bir** | Uzantı verileri | FK (Dış Anahtar) içeren ayrı tablo |
| **Bire-Çok** | Ebeveyn-çocuk ilişkisi | Çocuk tabloda FK |
| **Çoka-Çok** | Her iki tarafın da birden fazla bağlantısı varsa | Bağlantı (Junction) tablosu |

## Dış Anahtar (Foreign Key) ON DELETE Davranışı

```
├── CASCADE → Ebeveyn silindiğinde çocukları da sil
├── SET NULL → Çocukları yetim bırak (nullable ise)
├── RESTRICT → Çocuklar varsa ebeveynin silinmesini engelle
└── SET DEFAULT → Çocuklara varsayılan değerleri ata
```
