# Versiyonlama Stratejileri

> API'nizin gelecekteki evrimi için ilk günden planlama yapın.

## Karar Faktörleri

| Strateji | Uygulama | Avantaj/Dezavantaj |
|----------|---------------|------------|
| **URI** | /v1/users | Net, kolay önbelleğe alma |
| **Header** | Accept-Version: 1 | Temiz URL'ler, zor keşfedilebilirlik |
| **Query Parameter** | ?version=1 | Eklenmesi kolay, URL'yi karmaşıklaştırır |
| **Hiçbiri (None)** | Dikkatli evrim | Dahili API'ler için uygun, genel API'ler için riskli |

## Versiyonlama Felsefesi

```
Şunları değerlendirin:
├── Herkese açık (Public) API? → Versiyonlama URI içinde olmalı
├── Sadece dahili (Internal) kullanım? → Versiyonlamaya gerek olmayabilir
├── GraphQL? → Genellikle versiyonlanmaz (şema evrilir)
├── tRPC? → Tipler (TS) uyumluluğu zorunlu kılar
```
