# Migrasyon Prensipleri

> Sıfır kesinti (zero-downtime) ile güvenli şema değişikliği stratejisi.

## Güvenli Migrasyon Stratejisi

```
Kesintisiz değişiklikler için:
│
├── Sütun ekleme
│   └── Nullable olarak ekle → verileri doldur → NOT NULL ekle
│
├── Sütun silme
│   └── Kullanmayı bırak → yayına al → sütunu sil
│
├── İndeks ekleme
│   └── CREATE INDEX CONCURRENTLY (diğer işlemleri engellemez)
│
└── Sütun adını değiştirme (Rename)
    └── Yeni sütun ekle → veriyi taşı → yayına al → eskiyi sil
```

## Migrasyon Felsefesi

- Kırılmaya yol açacak (breaking changes) değişiklikleri asla tek adımda yapmayın.
- Migrasyonları önce verinin bir kopyasında test edin.
- Her zaman geri alma (rollback) planınız olsun.
- Mümkünse işlemlerinizi TRANSACTION bloğu içinde çalıştırın.

## Sunucusuz (Serverless) Veritabanları

### Neon (Serverless PostgreSQL)

| Özellik | Fayda |
|---------|---------|
| Scale to zero | Maliyet tasarrufu |
| Anlık dallanma (Instant branching) | Geliştirme/önizleme ortamları |
| Tam PostgreSQL desteği | Uyumluluk |
| Otomatik ölçeklendirme | Trafik yönetimi |

### Turso (Edge SQLite)

| Özellik | Fayda |
|---------|---------|
| Edge lokasyonları | Çok düşük gecikme süresi |
| SQLite uyumlu | Basitlik |
| Cömert ücretsiz katman | Düşük maliyet |
| Küresel dağıtım | Performans |
