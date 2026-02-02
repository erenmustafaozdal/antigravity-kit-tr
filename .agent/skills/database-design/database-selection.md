# Veritabanı Seçimi (2025)

> Veritabanını varsayılanlara göre değil, bağlama göre seçin.

## Karar Ağacı

```
Gereksinimleriniz nelerdir?
│
├── Tam ilişkisel özellikler gerekiyor
│   ├── Kendi sunucumuz (Self-hosted) → PostgreSQL
│   └── Sunucusuz (Serverless) → Neon, Supabase
│
├── Edge dağıtımı / Çok düşük gecikme
│   └── Turso (edge üzerinde SQLite)
│
├── YZ / Vektör arama
│   └── PostgreSQL + pgvector
│
├── Basit / Yerleşik (Embedded) / Yerel
│   └── SQLite
│
└── Küresel dağıtım
    └── PlanetScale, CockroachDB, Turso
```

## Karşılaştırma

| Veritabanı | En İyi Kullanım | Takaslar (Trade-offs) |
|----------|----------|------------|
| **PostgreSQL** | Tam özellikli, karmaşık sorgular | Barındırma gerektirir |
| **Neon** | Serverless PG, dallanma (branching) | PG karmaşıklığı |
| **Turso** | Edge, düşük gecikme | SQLite kısıtlamaları |
| **SQLite** | Basit, gömülü, yerel | Tek yazıcı (single-writer) kısıtı |
| **PlanetScale** | MySQL, küresel ölçek | Dış anahtar (foreign key) kısıtlamaları |

## Sorulacak Sorular

1. Dağıtım (deployment) ortamı nedir?
2. Sorgular ne kadar karmaşık?
3. Edge/serverless desteği önemli mi?
4. Vektör arama gerekiyor mu?
5. Küresel dağıtım şart mı?
