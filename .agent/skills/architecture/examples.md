# Mimari Örnekleri

> Proje türüne göre gerçek dünya mimari kararları.

---

## Örnek 1: MVP E-ticaret (Tek Geliştirici)

```yaml
Gereksinimler:
  - Başlangıçta <1000 kullanıcı
  - Tek (solo) geliştirici
  - Hızlı teslimat (8 hafta)
  - Bütçe kısıtlı

Mimari Kararlar:
  Uygulama Yapısı: Monolit (tek kişi için daha basit)
  Framework: Next.js (full-stack, hızlı)
  Veri Katmanı: Doğrudan Prisma (aşırı soyutlama yok)
  Kimlik Doğrulama: JWT (OAuth'tan daha basit)
  Ödeme: Stripe (hazır çözüm)
  Veritabanı: PostgreSQL (siparişler için ACID garantisi)

Kabul Edilen Takaslar:
  - Monolit → Bağımsız ölçeklenemez (ekip büyüklüğü bunu gerektirmiyor)
  - Repository yok → Daha az test edilebilir (basit CRUD için gerek yok)
  - JWT → Başlangıçta sosyal giriş yok (daha sonra eklenebilir)

Gelecek Planı:
  - Kullanıcı > 10K → Ödeme servisini ayır
  - Ekip > 3 → Repository desenini ekle
  - Sosyal giriş talebi → OAuth entegrasyonu yap
```

---

## Örnek 2: SaaS Ürünü (5-10 Geliştirici)

```yaml
Gereksinimler:
  - 1K-100K kullanıcı
  - 5-10 geliştirici
  - Uzun vadeli (12+ ay)
  - Çoklu etki alanları (faturalandırma, kullanıcılar, çekirdek özellikler)

Mimari Kararlar:
  Uygulama Yapısı: Modüler Monolit (ekip boyutu için optimal)
  Framework: NestJS (doğuştan modüler yapıda)
  Veri Katmanı: Repository deseni (test edilebilirlik, esneklik)
  Alan Modeli: Kısmi DDD (zengin varlıklar)
  Kimlik Doğrulama: OAuth + JWT
  Önbellek: Redis
  Veritabanı: PostgreSQL

Kabul Edilen Takaslar:
  - Modüler Monolit → Bazı modüller arası sıkı bağlar (mikroservislere henüz gerek yok)
  - Kısmi DDD → Tam "aggregates" yapısı yok (alan uzmanı eksikliği)
  - Sonradan RabbitMQ → Başlangıçta senkron iletişim (ihtiyaç olduğunda eklenecek)

Gelecek Planı:
  - Ekip > 10 → Mikroservislere geçişi değerlendir
  - Alanlar arası çakışma → Sınırlı bağlamları (bounded contexts) ayrıştır
  - Okuma performans sorunları → CQRS ekle
```

---

## Örnek 3: Kurumsal (100K+ Kullanıcı)

```yaml
Gereksinimler:
  - 100K+ kullanıcı
  - 10+ geliştirici
  - Çoklu iş alanları
  - Farklı ölçeklenme ihtiyaçları
  - 7/24 erişilebilirlik

Mimari Kararlar:
  Uygulama Yapısı: Mikroservisler (bağımsız ölçeklendirme)
  API Gateway: Kong/AWS API GW
  Alan Modeli: Tam DDD
  Tutarlılık: Olay güdümlü (nihai tutarlılık kabul edilebilir)
  Mesaj Kuyruğu: Kafka
  Kimlik Doğrulama: OAuth + SAML (kurumsal SSO)
  Veritabanı: Polyglot (her iş için doğru araç)
  CQRS: Seçili servislerde

Operasyonel Gereksinimler:
  - Service mesh (Istio/Linkerd)
  - Dağıtık izleme (Jaeger/Tempo)
  - Merkezi loglama (ELK/Loki)
  - Devre kesiciler (Circuit breakers - Resilience4j)
  - Kubernetes/Helm
```
