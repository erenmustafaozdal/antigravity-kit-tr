# Teknoloji Yığını Seçimi (2026)

> Web uygulamaları için varsayılan ve alternatif teknoloji seçenekleri.

## Varsayılan Yığın (Web Uygulaması - 2026)

```yaml
Ön Yüz (Frontend):
  framework: Next.js 16 (Kararlı)
  dil: TypeScript 5.7+
  stil: Tailwind CSS v4
  durum yönetimi: React 19 Actions / Server Components
  paketleyici: Turbopack (Geliştirme için Kararlı)

Arka Yüz (Backend):
  çalışma ortamı: Node.js 23
  framework: Next.js API Rotaları / Hono (Edge için)
  doğrulama: Zod / TypeBox

Veritabanı:
  birincil: PostgreSQL
  orm: Prisma / Drizzle
  barındırma: Supabase / Neon

Kimlik Doğrulama (Auth):
  sağlayıcı: Auth.js (v5) / Clerk

Monorepo:
  araç: Turborepo 2.0
```

## Alternatif Seçenekler

| İhtiyaç | Varsayılan | Alternatif |
|------|---------|-------------|
| Gerçek zamanlı | - | Supabase Realtime, Socket.io |
| Dosya depolama | - | Cloudinary, S3 |
| Ödeme | Stripe | LemonSqueezy, Paddle |
| E-posta | - | Resend, SendGrid |
| Arama | - | Algolia, Typesense |
