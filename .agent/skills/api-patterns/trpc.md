# tRPC Prensipleri

> TypeScript monorepo projeleri için uçtan uca (end-to-end) tip güvenliği.

## Ne Zaman Kullanılmalı?

```
✅ Mükemmel Uyum:
├── Hem ön yüz hem arka yüz TypeScript ise
├── Monorepo yapısı mevcutsa
├── Dahili (internal) araçlar geliştiriliyorsa
├── Hızlı geliştirme (rapid development) gerekiyorsa
└── Tip güvenliği kritikse

❌ Uygun Değildir:
├── TypeScript olmayan istemciler (native Android, iOS vb. eğer TS değilse)
├── Herkese açık (public) API'ler
├── REST standartlarına tam uyum gerekiyorsa
├── Arka yüzde farklı diller kullanılıyorsa
```

## Temel Avantajlar

```
Neden tRPC:
├── Sıfır şema bakımı (Zero schema maintenance)
├── Uçtan uca tip çıkarımı (End-to-end type inference)
├── Tüm teknoloji yığınında IDE otomatik tamamlama desteği
├── API değişikliklerinin anında yansıtılması
├── Kod oluşturma (code generation) adımına ihtiyaç duyulmaması
```

## Entegrasyon Desenleri

```
Yaygın Kurulumlar:
├── Next.js + tRPC (en yaygın kullanım)
├── Paylaşılan tiplere sahip Monorepo yapıları
├── Herhangi bir TS ön yüz + arka yüz kombinasyonu
```
