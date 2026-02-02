# API Stili Seçimi (2025)

> REST vs GraphQL vs tRPC - Hangi durumda hangisi seçilmeli?

## Karar Ağacı

```
API tüketicileri (istemciler) kim?
│
├── Herkese Açık (Public) API / Çoklu Platformlar
│   └── REST + OpenAPI (en geniş uyumluluk)
│
├── Karmaşık veri ihtiyaçları / Çoklu ön yüzler (frontends)
│   └── GraphQL (esnek sorgular)
│
├── TypeScript ön yüz + arka yüz (Monorepo)
│   └── tRPC (uçtan uca tip güvenliği)
│
├── Gerçek zamanlı (Real-time) / Olay güdümlü (Event-driven)
│   └── WebSocket + AsyncAPI
│
└── Dahili mikro servisler
    └── gRPC (performans) veya REST (basitlik)
```

## Karşılaştırma Matrisi

| Faktör | REST | GraphQL | tRPC |
|--------|------|---------|------|
| **En İyi Kullanım** | Herkese Açık API'ler | Karmaşık Uygulamalar | TS Monorepo projeleri |
| **Öğrenme Eğrisi** | Düşük | Orta | Düşük (TS biliyorsanız) |
| **Gereksiz/Eksik Veri Çekme** | Yaygın | Çözülmüş | Çözülmüş |
| **Tip Güvenliği** | Manuel (OpenAPI) | Şema tabanlı | Otomatik |
| **Önbelleğe Alma** | HTTP yerel | Karmaşık | İstemci tabanlı |

## Seçim Soruları

1. API tüketicileri (istemciler) kimler olacak?
2. Ön yüzde (frontend) TypeScript kullanılıyor mu?
3. Veri ilişkileri ne kadar karmaşık?
4. HTTP seviyesinde önbelleğe alma (caching) kritik mi?
5. API herkese açık mı olacak yoksa sadece dahili kullanım için mi?
