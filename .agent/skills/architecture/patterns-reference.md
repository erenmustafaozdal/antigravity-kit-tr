# Mimari Desenler Referansı

> Yaygın desenler için kullanım rehberi ve hızlı referans.

## Veri Erişim Desenleri

| Desen | Ne Zaman Kullanılmalı | Ne Zaman Kullanılmamalı | Karmaşıklık |
|---------|-------------|-----------------|------------|
| **Active Record** | Basit CRUD, hızlı prototipleme | Karmaşık sorgular, çoklu kaynaklar | Düşük |
| **Repository** | Test ihtiyacı, çoklu kaynaklar | Basit CRUD, tek veritabanı | Orta |
| **Unit of Work** | Karmaşık işlemler (transactions) | Basit operasyonlar | Yüksek |
| **Data Mapper** | Karmaşık alan (domain), performans | Basit CRUD, hızlı geliştirme | Yüksek |

## Alan Mantığı (Domain Logic) Desenleri

| Desen | Ne Zaman Kullanılmalı | Ne Zaman Kullanılmamalı | Karmaşıklık |
|---------|-------------|-----------------|------------|
| **Transaction Script** | Basit CRUD, prosedürel yapı | Karmaşık iş kuralları | Düşük |
| **Table Module** | Kayıt tabanlı mantık | Zengin davranış ihtiyacı | Düşük |
| **Domain Model** | Karmaşık iş mantığı | Basit CRUD | Orta |
| **DDD (Tam)** | Karmaşık alan, alan uzmanları varlığı | Basit alanlar, uzman yokluğu | Yüksek |

## Dağıtık Sistem Desenleri

| Desen | Ne Zaman Kullanılmalı | Ne Zaman Kullanılmamalı | Karmaşıklık |
|---------|-------------|-----------------|------------|
| **Modüler Monolit** | Küçük ekipler, belirsiz sınırlar | Net bağlamlar, farklı ölçekler | Orta |
| **Mikroservisler** | Farklı ölçekler, büyük ekipler | Küçük ekipler, basit alanlar | Çok Yüksek |
| **Olay Güdümlü** | Gerçek zamanlı, gevşek bağlılık | Basit iş akışları, güçlü tutarlılık | Yüksek |
| **CQRS** | Yazma/okuma performansı ayrımları | Basit CRUD, aynı model | Yüksek |
| **Saga** | Dağıtık işlemler (transactions) | Tek veritabanı, basit ACID | Yüksek |

## API Desenleri

| Desen | Ne Zaman Kullanılmalı | Ne Zaman Kullanılmamalı | Karmaşıklık |
|---------|-------------|-----------------|------------|
| **REST** | Standart CRUD, kaynaklar | Gerçek zamanlı, karmaşık sorgular | Düşük |
| **GraphQL** | Esnek sorgular, çoklu istemciler | Basit CRUD, önbellek ihtiyacı | Orta |
| **gRPC** | Dahili servisler, performans | Genel API'ler, tarayıcı istemcileri | Orta |
| **WebSocket** | Gerçek zamanlı güncellemeler | Basit istek/yanıt yapısı | Orta |

---

## Basitlik Prensibi

**"Basit başlayın, karmaşıklığı sadece gerekli olduğu kanıtlandığında ekleyin."**

- Desenleri daha sonra her zaman ekleyebilirsiniz.
- Karmaşıklığı kaldırmak, eklemekten ÇOK daha zordur.
- Kararsız kaldığınızda, daha basit olan seçeneği tercih edin.
