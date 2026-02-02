# İndeksleme Prensipleri

> İndekslerin ne zaman ve nasıl etkin bir şekilde oluşturulacağı.

## Ne Zaman İndeks Oluşturulmalı?

```
Şu sütunları indeksleyin:
├── WHERE ifadelerinde kullanılan sütunlar
├── JOIN koşullarında kullanılan sütunlar
├── ORDER BY içinde kullanılan sütunlar
├── Dış anahtar (Foreign key) sütunları
└── Benzersizlik (Unique) kısıtlamaları

Aşırı indekslemeden kaçının:
├── Yazma ağırlıklı tablolar (ekleme işlemleri yavaşlar)
├── Düşük kardinaliteli (tekrarlı veri çok olan) sütunlar
├── Nadiren sorgulanan sütunlar
```

## İndeks Türü Seçimi

| Tür | Kullanım Alanı |
|------|---------|
| **B-tree** | Genel amaçlı, eşitlik ve aralık sorguları |
| **Hash** | Sadece eşitlik sorguları, daha hızlı |
| **GIN** | JSONB, diziler, tam metin (full-text) |
| **GiST** | Geometrik veriler, aralık tipleri |
| **HNSW/IVFFlat** | Vektör benzerliği (pgvector) |

## Bileşik İndeks Prensipleri

```
Bileşik indekslerde sıralama önemlidir:
├── Eşitlik sorgulanan sütunlar önce
├── Aralık (range) sorgulanan sütunlar sonra
├── En seçici (en benzersiz veri dönecek olan) sütunlar önce
└── Sorgu desenleriyle eşleşen sıralama
```
