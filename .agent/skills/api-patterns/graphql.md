# GraphQL Prensipleri

> Karmaşık ve birbiriyle bağlantılı veriler için esnek sorgular.

## Ne Zaman Kullanılmalı?

```
✅ Uygundur:
├── Karmaşık, birbiriyle bağlantılı veriler
├── Çoklu ön yüz (frontend) platformları
├── İstemcilerin esnek sorgulara ihtiyaç duyması
├── Sürekli evrilen veri gereksinimleri
└── Gereksiz veri çekimini (over-fetching) azaltmak kritikse

❌ Uygun Değildir:
├── Basit CRUD işlemleri
├── Dosya yükleme ağırlıklı işlemler
├── HTTP seviyesinde önbelleğe alma (caching) çok önemliyse
├── Ekibin GraphQL tecrübesi yoksa
```

## Şema Tasarım Prensipleri

```
Prensipler:
├── Uç noktalar yerine grafiksel düşünün
├── Gelişebilirliğe göre tasarlayın (versiyonlama yerine)
├── Sayfalama için "connections" kullanın
├── Tipler konusunda spesifik olun (genel "data" tipi yerine)
├── Boş olabilirliği (nullability) dikkatli yönetin
```

## Güvenlik Değerlendirmeleri

```
Şunlara karşı koruma sağlayın:
├── Sorgu derinliği saldırıları → Maksimum derinlik belirleyin
├── Sorgu karmaşıklığı → Maliyet hesaplaması yapın
├── Toplu işlem (Batching) suiistimali → Paket boyutunu sınırlayın
├── İnceleme (Introspection) → Prodüksiyon ortamında devre dışı bırakın
```
