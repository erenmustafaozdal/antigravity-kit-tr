# ORM Seçimi (2025)

> Dağıtım ortamına ve geliştirici deneyimi (DX) ihtiyaçlarına göre ORM seçin.

## Karar Ağacı

```
Bağlam nedir?
│
├── Edge dağıtımı / Paket boyutu (bundle size) önemli
│   └── Drizzle (en küçük, SQL benzeri)
│
├── En iyi DX / Önce şema (Schema-first)
│   └── Prisma (migrasyonlar, yönetim paneli/studio)
│
├── Maksimum kontrol
│   └── Query builder ile ham SQL
│
└── Python ekosistemi
    └── SQLAlchemy 2.0 (async desteği)
```

## Karşılaştırma

| ORM | En İyi Kullanım | Takaslar (Trade-offs) |
|-----|----------|------------|
| **Drizzle** | Edge, TypeScript | Daha yeni, daha az kaynak/örnek |
| **Prisma** | DX, şema yönetimi | Daha ağır, "edge" için her zaman uygun değil |
| **Kysely** | Tip güvenli SQL oluşturucu | Manuel migrasyon yönetimi |
| **Ham SQL** | Karmaşık sorgular, tam kontrol | Manuel tip güvenliği yönetimi |
