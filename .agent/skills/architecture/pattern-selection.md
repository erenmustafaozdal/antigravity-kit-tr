# Desen Seçim Yönergeleri

> Mimari desenleri seçmek için karar ağaçları.

## Ana Karar Ağacı

```
BAŞLA: Temel odak noktanız nedir?

┌─ Veri Erişim Karmaşıklığı mı?
│  ├─ YÜKSEK (karmaşık sorgular, test ihtiyacı)
│  │  → Repository Pattern + Unit of Work
│  │  DOĞRULA: Veri kaynağı sık değişecek mi?
│  │     ├─ EVET → Repository katmanı eklemeye değer
│  │     └─ HAYIR → Daha basit olan doğrudan ORM erişimini düşünün
│  └─ DÜŞÜK (basit CRUD, tek veritabanı)
│     → Doğrudan ORM (Prisma, Drizzle vb.)
│     Daha Basit = Daha İyi, Daha Hızlı
│
├─ İş Kuralları (Business Rules) Karmaşıklığı mı?
│  ├─ YÜKSEK (alan mantığı, bağlama göre değişen kurallar)
│  │  → Etki Alanı Odaklı Tasarım (Domain-Driven Design - DDD)
│  │  DOĞRULA: Ekipte alan uzmanları (domain experts) var mı?
│  │     ├─ EVET → Tam DDD (Aggregates, Value Objects)
│  │     └─ HAYIR → Kısmi DDD (zengin varlıklar, net sınırlar)
│  └─ DÜŞÜK (çoğunlukla CRUD, basit doğrulama)
│     → Transaction Script deseni
│     Daha Basit = Daha İyi, Daha Hızlı
│
├─ Bağımsız Ölçeklendirme İhtiyacı mı?
│  ├─ EVET (farklı bileşenler farklı ölçeklenmeli)
│  │  → Mikroservisler - Karmaşıklığa DEĞER
│  │  GEREKSİNİMLER (HEPSİ doğru olmalı):
│  │    - Net etki alanı sınırları
│  │    - Ekip > 10 geliştirici
│  │    - Servis başına farklı ölçeklenme ihtiyaçları
│  │  HEPSİ KARŞILANMIYORSA → Modüler Monolit (Modular Monolith)
│  └─ HAYIR (her şey birlikte ölçekleniyor)
│     → Modüler Monolit
│     İhtiyaç duyulduğu kanıtlandığında servisler daha sonra ayrılabilir
│
└─ Gerçek Zamanlı (Real-time) Gereksinimler mi?
   ├─ YÜKSEK (anlık güncellemeler, çoklu kullanıcı senkronizasyonu)
   │  → Olay Güdümlü Mimari (Event-Driven Architecture)
   │  → Mesaj Kuyruğu (RabbitMQ, Redis, Kafka)
   │  DOĞRULA: Nihai tutarlılığı (eventual consistency) yönetebilir misiniz?
   │     ├─ EVET → Olay güdümlü mimari uygundur
   │     └─ HAYIR → Polling ile senkron iletişim
   └─ DÜŞÜK (nihai tutarlılık kabul edilebilir)
      → Senkron (REST/GraphQL)
      Daha Basit = Daha İyi, Daha Hızlı
```

## Desen Seçmeden Önce 3 Soru

1. **Çözülen Sorun**: Bu desen TAM OLARAK hangi sorunu çözüyor?
2. **Daha Basit Alternatif**: Daha basit bir çözüm var mı?
3. **Ertelenebilir Karmaşıklık**: Bunu daha sonra ihtiyaç olduğunda ekleyebilir miyiz?

## Kırmızı Bayraklar (Anti-desenler)

| Desen | Anti-desen | Daha Basit Alternatif |
|---------|-------------|-------------------|
| Mikroservisler | Erken parçalama | Monolit ile başla, sonra ayır |
| Clean/Hexagonal | Aşırı soyutlama | Önce somut yapılar, sonra arayüzler |
| Event Sourcing | Fazla mühendislik | Sadece ekleme (append-only) yapılan denetim logu |
| CQRS | Gereksiz karmaşıklık | Tekil model |
| Repository | Basit CRUD için YAGNI | Doğrudan ORM erişimi |
