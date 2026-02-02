# Proje İskeleti (Project Scaffolding)

> Yeni projeler için dizin yapısı ve temel dosyalar.

---

## Next.js Full-Stack Yapısı (2025 Optimize Edilmiş)

```
proje-adi/
├── src/
│   ├── app/                        # Sadece rotalar (ince katman)
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── globals.css
│   │   ├── (auth)/                 # Rota grubu - giriş/kayıt sayfaları
│   │   │   ├── login/page.tsx
│   │   │   └── register/page.tsx
│   │   ├── (dashboard)/            # Rota grubu - panel düzeni
│   │   │   ├── layout.tsx
│   │   │   └── page.tsx
│   │   └── api/
│   │       └── [resource]/route.ts
│   │
│   ├── features/                   # Özellik tabanlı modüller
│   │   ├── auth/
│   │   │   ├── components/
│   │   │   ├── hooks/
│   │   │   ├── actions.ts          # Server Actions
│   │   │   ├── queries.ts          # Veri çekme (Data fetching)
│   │   │   └── types.ts
│   │   ├── products/
│   │   │   ├── components/
│   │   │   ├── actions.ts
│   │   │   └── queries.ts
│   │   └── cart/
│   │       └── ...
│   │
│   ├── shared/                     # Paylaşılan araçlar
│   │   ├── components/ui/          # Tekrar kullanılabilir UI bileşenleri
│   │   ├── lib/                    # Yardımcı kütüphaneler, araçlar
│   │   └── hooks/                  # Global hook'lar
│   │
│   └── server/                     # Sadece sunucu taraflı kodlar
│       ├── db/                     # Veritabanı istemcisi (Prisma vb.)
│       ├── auth/                   # Auth yapılandırması
│       └── services/               # Harici API entegrasyonları
│
├── prisma/
│   ├── schema.prisma
│   ├── migrations/
│   └── seed.ts
│
├── public/
├── .env.example
├── .env.local
├── package.json
├── tailwind.config.ts
├── tsconfig.json
└── README.md
```

---

## Yapı Prensipleri

| Prensip | Uygulama |
|-----------|----------------|
| **Özellik İzolasyonu** | `features/` altında her özelliğin kendi bileşenleri, hook'ları ve action'ları bulunur |
| **Server/Client Ayrımı** | Sadece sunucu kodları `server/` içindedir, istemciye yanlışlıkla aktarılması önlenir |
| **İnce Rotalar** | `app/` sadece yönlendirme içindir, mantık `features/` altında yaşar |
| **Rota Grupları** | `(grupAdi)/` yapısı, URL'yi etkilemeden düzen (layout) paylaşımı sağlar |
| **Paylaşılan Kod** | `shared/` gerçekten tekrar kullanılabilen UI ve araçlar içindir |

---

## Temel Dosyalar

| Dosya | Amacı |
|------|---------|
| `package.json` | Bağımlılıklar ve scriptler |
| `tsconfig.json` | TypeScript ayarları ve yol takma adları (`@/features/*`) |
| `tailwind.config.ts` | Tailwind CSS yapılandırması |
| `.env.example` | Ortam değişkenleri şablonu |
| `README.md` | Proje dokümantasyonu |
| `.gitignore` | Git tarafından yoksayılacak dosyalar |
| `prisma/schema.prisma`| Veritabanı şeması |

---

## Yol Takma Adları (Path Aliases - tsconfig.json)

```json
{
  "compilerOptions": {
    "paths": {
      "@/*": ["./src/*"],
      "@/features/*": ["./src/features/*"],
      "@/shared/*": ["./src/shared/*"],
      "@/server/*": ["./src/server/*"]
    }
  }
}
```

---

## Ne Nerede Olmalı?

| İhtiyaç | Konum |
|------|----------|
| Yeni sayfa/rota | `app/(grup)/page.tsx` |
| Özelliğe özel bileşen | `features/[isim]/components/` |
| Server action | `features/[isim]/actions.ts` |
| Veri çekme mantığı | `features/[isim]/queries.ts` |
| Genel buton/input vb. | `shared/components/ui/` |
| Veritabanı sorgusu | `server/db/` |
| Harici API çağrısı | `server/services/` |
