# Sorgu Optimizasyonu

> N+1 problemi, EXPLAIN ANALYZE ve optimizasyon öncelikleri.

## N+1 Problemi

```
N+1 Nedir?
├── Ebeveyn kayıtları almak için 1 sorgu
├── İlişkili kayıtları almak için N adet sorgu
└── Çok yavaştır!

Çözümler:
├── JOIN → Tüm veriyi tek sorgu ile getir
├── Eager loading → ORM'in JOIN yapmasını sağla
├── DataLoader → Toplu (batch) ve önbellekli çekim (GraphQL)
├── Alt Sorgu (Subquery) → İlişkili verileri tek bir toplu sorguyla çek
```

## Sorgu Analizi Bakış Açısı

```
Optimize etmeden önce:
├── Sorguyu EXPLAIN ANALYZE ile çalıştır
├── "Seq Scan" (tam tablo taraması) var mı bak
├── Gerçek vs tahmini satır sayılarını kontrol et
├── Eksik indeksleri tespit et
```

## Optimizasyon Öncelikleri

1. **Eksik indeksleri ekleyin** (en yaygın sorun)
2. **Sadece gereken sütunları seçin** (SELECT * yerine)
3. **Uygun JOIN'leri kullanın** (mümkünse alt sorgulardan kaçının)
4. **Erken limitleyin** (sayfalamayı veritabanı seviyesinde yapın)
5. **Önbelleğe alın** (uygun görüldüğünde)
