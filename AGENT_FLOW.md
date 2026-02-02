# 🔄 Ajan Akış Mimarisi

> **Antigravity Kit** - Kapsamlı YZ Ajan İş Akışı Dokümantasyonu

---

## 📊 Genel Akış Şeması

```
┌─────────────────────────────────────────────────────────────────┐
│                        KULLANICI İSTEĞİ                          │
└────────────────────────────┬────────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────────┐
│                    İSTEK SINIFLANDIRMA                           │
│  • Niyeti analiz et (inşa et, hata ayıkla, test et, yayınla vb.)│
│  • Alanı belirle (frontend, backend, mobil, vb.)                │
│  • Karmaşıklığı tespit et (basit, orta, karmaşık)               │
└────────────────────────────┬────────────────────────────────────┘
                             │
                ┌────────────┴────────────┐
                │                         │
                ▼                         ▼
    ┌───────────────────┐      ┌──────────────────┐
    │  İŞ AKIŞI KOMUTU  │      │  DOĞRUDAN AJAN   │
    │   (Slash Komutu)  │      │     ATAMASI      │
    └─────────┬─────────┘      └────────┬─────────┘
              │                         │
              ▼                         ▼
    ┌───────────────────┐      ┌──────────────────┐
    │ /brainstorm       │      │ Alan Bazlı       │
    │ /create           │      │ Ajan Seçimi      │
    │ /debug            │      │                  │
    │ /deploy           │      │ • frontend-*     │
    │ /enhance          │      │ • backend-*      │
    │ /orchestrate      │      │ • mobile-*       │
    │ /plan             │      │ • database-*     │
    │ /preview          │      │ • devops-*       │
    │ /status           │      │ • test-*         │
    │ /test             │      │ • security-*     │
    │ /ui-ux-pro-max    │      │ • game-*         │
    └─────────┬─────────┘      └────────┬─────────┘
              │                         │
              └────────────┬────────────┘
                           │
                           ▼
         ┌─────────────────────────────────────┐
         │          AJAN BAŞLATMA              │
         │  • Ajan personasını/rolünü yükle    │
         │  • Gerekli yetenekleri yükle        │
         │  • Davranış modunu ayarla           │
         └──────────────┬──────────────────────┘
                        │
                        ▼
         ┌─────────────────────────────────────┐
         │      YETENEK YÜKLEME PROTOKOLÜ      │
         │                                     │
         │  1. SKILL.md üst verisini oku       │
         │  2. referansları yükle (gerekirse)  │
         │  3. scriptleri çalıştır (gerekirse) │
         │  4. Kural ve desenleri uygula       │
         └──────────────┬──────────────────────┘
                        │
                        ▼
         ┌─────────────────────────────────────┐
         │          GÖREV YÜRÜTME              │
         │                                     │
         │  • Kod tabanını analiz et           │
         │  • En iyi uygulamaları uygula       │
         │  • Kod üret/değiştir                │
         │  • Doğrulamaları çalıştır           │
         │  • Testleri çalıştır                │
         └──────────────┬──────────────────────┘
                        │
                        ▼
         ┌─────────────────────────────────────┐
         │         DOĞRULAMA KATMANI           │
         │                                     │
         │  Hızlı Kontrol (checklist.py):      │
         │  • Güvenlik taraması                │
         │  • Kod kalitesi (lint/türler)       │
         │  • Şema doğrulama                   │
         │  • Test paketi                      │
         │  • UX denetimi                      │
         │  • SEO kontrolü                     │
         │                                     │
         │  Tam Kontrol (verify_all.py):       │
         │  • Yukarıdakilerin hepsi + Lighthouse│
         │  • Uçtan Uca (E2E) testler          │
         │  • Bundle analizi                   │
         │  • Mobil denetimi                   │
         │  • i18n kontrolü                    │
         └──────────────┬──────────────────────┘
                        │
                        ▼
         ┌─────────────────────────────────────┐
         │           SONUÇ TESLİMİ             │
         │  • Değişiklikleri kullanıcıya sun   │
         │  • Açıklamalar sağla                │
         │  • Sonraki adımları öner            │
         └─────────────────────────────────────┘
```

---

## 🎯 Detaylı Ajan İş Akışı

### 1️⃣ **İstek Giriş Noktaları**

```
Kullanıcı Girdi Tipleri:
┌─────────────────────────────────────────────────────────────┐
│ A. Doğal Dil İsteği                                         │
│    "Grafikli bir React paneli oluştur"                      │
│                                                             │
│ B. Slash Komutu                                             │
│    "/create özellik: kullanıcı kimlik doğrulama"            │
│                                                             │
│ C. Alan Bazlı İstek                                         │
│    "Veritabanı sorgularını optimize et" → database-architect│
│    "Güvenlik açığını düzelt" → security-auditor             │
│    "AWS'ye dağıt" → devops-engineer                         │
└─────────────────────────────────────────────────────────────┘
```

#### Sokratik Kapı Protokolü

Uygulamadan önce doğrulayın:

- **Yeni Özellik** → 3 stratejik soru SOR
- **Hata Düzeltme** → Anlayışı doğrula + etkiyi sor
- **Belirsiz İstek** → Amaç, Kullanıcılar ve Kapsamı sor

### 2️⃣ **Ajan Seçim Matrisi**

#### Ajan Yönlendirme Kontrol Listesi (Zorunlu)

HERHANGİ bir kod/tasarım işinden önce:

| Adım | Kontrol                      | İşaretlenmemişse                         |
| ---- | ---------------------------- | ---------------------------------------- |
| 1    | Doğru ajanı belirle          | → İstek alanını analiz et                |
| 2    | Ajanın .md dosyasını oku     | → `.agent/agents/{agent}.md` dosyasını aç|
| 3    | Ajanı duyur                  | → `🤖 @[agent] bilgisi uygulanıyor...`   |
| 4    | Frontmatter'dan yetenek yükle| → `skills:` alanını kontrol et           |

```
İstek Alanı → Ajan Eşleşmesi:

┌──────────────────────┬─────────────────────┬──────────────────────────┐
│ Alan                 │ Birincil Ajan       │ Yüklenen Yetenekler      │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ UI/UX Tasarım        │ frontend-specialist │ react-best-practices      │
│                      │                     │ frontend-design          │
│                      │                     │ tailwind-patterns        │
│                      │                     │ web-design-guidelines    │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ API Geliştirme       │ backend-specialist  │ api-patterns             │
│                      │                     │ nodejs-best-practices    │
│                      │                     │ nestjs-expert            │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Veritabanı Tasarımı  │ database-architect  │ database-design          │
│                      │                     │ prisma-expert            │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Mobil Uygulama       │ mobile-developer    │ mobile-design            │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Oyun Geliştirme      │ game-developer      │ game-development         │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ DevOps/Dağıtım       │ devops-engineer     │ docker-expert            │
│                      │                     │ deployment-procedures    │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Güvenlik Denetimi    │ security-auditor    │ vulnerability-scanner    │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Sızma Testi          │ penetration-tester  │ red-team-tactics         │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Test Etme            │ test-engineer       │ testing-patterns         │
│                      │                     │ webapp-testing           │
│                      │                     │ tdd-workflow             │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Hata Ayıklama        │ debugger            │ systematic-debugging     │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Performans           │ performance-        │ performance-profiling    │
│                      │ optimizer           │                          │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ SEO                  │ seo-specialist      │ seo-fundamentals         │
│                      │                     │ geo-fundamentals         │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Dokümantasyon        │ documentation-      │ documentation-templates  │
│                      │ writer              │                          │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Planlama/Keşif       │ project-planner     │ brainstorming            │
│                      │                     │ plan-writing             │
│                      │                     │ architecture             │
├──────────────────────┼─────────────────────┼──────────────────────────┤
│ Çoklu-Ajan Görevleri │ orchestrator        │ parallel-agents          │
│                      │                     │ behavioral-modes         │
└──────────────────────┴─────────────────────┴──────────────────────────┘
```

### 3️⃣ **Yetenek Yükleme Protokolü**

```
┌─────────────────────────────────────────────────────────────┐
│                   YETENEK YÜKLEME AKIŞI                      │
└─────────────────────────────────────────────────────────────┘

Adım 1: İsteği Yetenekle Eşleştir
┌──────────────────────────────────────────┐
│ Kullanıcı: "Bir REST API oluştur"        │
│   ↓                                      │
│ Anahtar Kelime: "API" → api-patterns     │
└──────────────────────────────────────────┘
                    ↓
Adım 2: Yetenek Üst Verisini Yükle
┌──────────────────────────────────────────┐
│ Oku: .agent/skills/api-patterns/         │
│       └── SKILL.md (ana talimatlar)      │
└──────────────────────────────────────────┘
                    ↓
Adım 3: Referansları Yükle (gerekirse)
┌──────────────────────────────────────────┐
│ Oku: api-patterns/rest.md                │
│       api-patterns/graphql.md            │
│       api-patterns/auth.md               │
│       api-patterns/documentation.md      │
└──────────────────────────────────────────┘
                    ↓
Adım 4: Scriptleri Çalıştır (gerekirse)
┌──────────────────────────────────────────┐
│ Çalıştır: scripts/api_validator.py       │
│           (API tasarımını doğrular)      │
└──────────────────────────────────────────┘
                    ↓
Adım 5: Bilgiyi Uygula
┌──────────────────────────────────────────┐
│ Ajan artık şunlara sahip:                │
│ • API tasarım desenleri                  │
│ • Kimlik doğrulama stratejileri          │
│ • Dokümantasyon şablonları               │
│ • Doğrulama scriptleri                   │
└──────────────────────────────────────────┘

### İlişkili Yetenekler Deseni

Yetenekler artık birbirine link verir:
- `frontend-design` → `web-design-guidelines` (kodlamadan sonra)
- `web-design-guidelines` → `frontend-design` (kodlamadan önce)

> **Not**: Scriptler otomatik çalıştırılmaz. YZ çalıştırılmasını önerir, kullanıcı onaylar.
```

### 4️⃣ **İş Akışı Komut Yürütme**

```
Slash Komut Akışı:

/brainstorm
    ↓
    1. Yükle: brainstorming yeteneği
    2. Uygula: Sokratik sorgulama
    3. Çıktı: Yapılandırılmış keşif belgesi

/create
    ↓
    1. Tespit Et: Proje tipi (web/mobil/api/oyun)
    2. Yükle: app-builder yeteneği + alan-bazlı yetenekler
    3. Seç: app-builder/templates/ içinden şablon
    4. İskelet: Proje yapısını oluştur
    5. Doğrula: checklist.py çalıştır

/debug
    ↓
    1. Yükle: systematic-debugging yeteneği
    2. Analiz Et: Hata logları, stack trace'ler
    3. Uygula: Kök neden analizi
    4. Öner: Kod örnekleriyle düzeltme
    5. Test Et: Düzeltmenin çalıştığını doğrula

/deploy
    ↓
    1. Yükle: deployment-procedures yeteneği
    2. Tespit Et: Platform (Vercel, AWS, Docker, vb.)
    3. Hazırla: Derleme çıktıları (artifacts)
    4. Yürüt: Dağıtım scriptleri
    5. Doğrula: Sağlık kontrolleri
    6. Çıktı: Dağıtım URL'si

/test
    ↓
    1. Yükle: testing-patterns + webapp-testing yetenekleri
    2. Tespit Et: Test framework'ü (Jest, Vitest, Playwright)
    3. Üret: Test senaryoları
    4. Yürüt: Testleri çalıştır
    5. Raporla: Kapsam + sonuçlar

/orchestrate
    ↓
    1. Yükle: parallel-agents yeteneği
    2. Parçala: Görevi alt görevlere böl
    3. Ata: Her alt görevi uzman ajana ata
    4. Koordine Et: Paralel yürütme
    5. Birleştir: Sonuçları bir araya getir
    6. Doğrula: Tam doğrulama çalıştır

/plan
    ↓
    1. Yükle: plan-writing + architecture yetenekleri
    2. Analiz Et: Gereksinimler
    3. Kırılım: Tahminlerle birlikte görevler
    4. Çıktı: Kilometre taşları içeren yapılandırılmış plan

/ui-ux-pro-max
    ↓
    1. Yükle: ui-ux-pro-max yeteneği
    2. Erişim: 50 tasarım stili
    3. Erişim: 21 renk paleti
    4. Erişim: 50 yazı tipi kombinasyonu
    5. Üret: Seçilen stille profesyonel UI
```

### 5️⃣ **Çoklu Ajan Orkestrasyonu**

```
Karmaşık Görev → /orchestrate → Çoklu Uzman Personalar

Örnek: "Full-stack bir e-ticaret uygulaması oluştur"

┌─────────────────────────────────────────────────────────────┐
│                     ORKESTRATÖR AJAN                         │
│  Görevi sıralı iş akışlarına böler                          │
└─────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌───────────────┐   ┌───────────────┐   ┌───────────────┐
│ FRONTEND      │   │ BACKEND       │   │ VERİTABANI    │
│ UZMANI        │   │ UZMANI        │   │ MİMARI        │
│               │   │               │   │               │
│ Yetenekler:   │   │ Yetenekler:   │   │ Yetenekler:   │
│ • react-*     │   │ • api-*       │   │ • database-*  │
│ • nextjs-*    │   │ • nodejs-*    │   │ • prisma-*    │
│ • tailwind-*  │   │ • nestjs-*    │   │               │
│               │   │               │   │               │
│ İnşa Eder:    │   │ İnşa Eder:    │   │ İnşa Eder:    │
│ • UI/UX       │   │ • REST API    │   │ • Şema        │
│ • Bileşenler  │   │ • Auth        │   │ • Migrasyonlar│
│ • Sayfalar    │   │ • İş Mantığı  │   │ • İndeksler   │
└───────┬───────┘   └───────┬───────┘   └───────┬───────┘
        │                   │                   │
        └─────────────────┬─┴───────────────────┘
                          │
                          ▼
        ┌─────────────────────────────────────┐
        │          KOD TUTARLILIĞI            │
        │  • YZ tutarlılığı korur             │
        │  • Sıralı bağlam geçişi             │
        │  • API kontratlarının eşleşmesi     │
        └──────────────┬──────────────────────┘
                       │
                       ▼
        ┌─────────────────────────────────────┐
        │       DOĞRULAMA (Tüm Ajanlar)       │
        │  • test-engineer → Testler          │
        │  • security-auditor → Güvenlik      │
        │  • performance-optimizer → Perf     │
        └──────────────┬──────────────────────┘
                       │
                       ▼
        ┌─────────────────────────────────────┐
        │             DAĞITIM                 │
        │  • devops-engineer → Yayınla        │
        └─────────────────────────────────────┘
```

### 6️⃣ **Doğrulama & Kalite Kapıları**

```
┌─────────────────────────────────────────────────────────────┐
│                  DOĞRULAMA HATTI                             │
└─────────────────────────────────────────────────────────────┘

Geliştirme Sırasında (Hızlı Kontroller):
┌──────────────────────────────────────────┐
│ python .agent/scripts/checklist.py .     │
├──────────────────────────────────────────┤
│ ✓ Güvenlik Taraması (zafiyetler)         │
│ ✓ Kod Kalitesi (ESLint, TypeScript)      │
│ ✓ Şema Doğrulama (Prisma/DB)             │
│ ✓ Test Paketi (Birim testleri)           │
│ ✓ UX Denetimi (Erişilebilirlik)          │
│ ✓ SEO Kontrolü (Meta etiketler, perf)    │
└──────────────────────────────────────────┘
        Süre: ~30 saniye

Dağıtım Öncesi (Tam Doğrulama):
┌──────────────────────────────────────────────────────┐
│ python .agent/scripts/verify_all.py .                │
│        --url http://localhost:3000                   │
├──────────────────────────────────────────────────────┤
│ ✓ Tüm Hızlı Kontroller                               │
│ ✓ Lighthouse Denetimi (Core Web Vitals)              │
│ ✓ Playwright E2E Testleri                            │
│ ✓ Bundle Analizi (Boyut, tree-shaking)               │
│ ✓ Mobil Denetimi (Responsive, dokunma hedefleri)     │
│ ✓ i18n Kontrolü (Çeviriler, yerel ayar)              │
└──────────────────────────────────────────────────────┘
        Süre: ~3-5 dakika
```

---

## 🧩 Yetenek-Script Eşleşmesi

```
Otomatik Scriptlere Sahip Yetenekler:

┌─────────────────────────┬──────────────────────────────────┐
│ Yetenek                 │ Script                           │
├─────────────────────────┼──────────────────────────────────┤
│ api-patterns            │ scripts/api_validator.py         │
│ database-design         │ scripts/schema_validator.py      │
│ frontend-design         │ scripts/accessibility_checker.py │
│                         │ scripts/ux_audit.py              │
│ geo-fundamentals        │ scripts/geo_checker.py           │
│ i18n-localization       │ scripts/i18n_checker.py          │
│ lint-and-validate       │ scripts/lint_runner.py           │
│                         │ scripts/type_coverage.py         │
│ mobile-design           │ scripts/mobile_audit.py          │
│ performance-profiling   │ scripts/lighthouse_runner.py     │
│                         │ scripts/bundle_analyzer.py       │
│ seo-fundamentals        │ scripts/seo_checker.py           │
│ testing-patterns        │ scripts/test_runner.py           │
│ vulnerability-scanner   │ scripts/security_scanner.py      │
│ webapp-testing          │ scripts/e2e_runner.py            │
└─────────────────────────┴──────────────────────────────────┘
```

---

## 🔄 Tam İstek Yaşam Döngüsü Örneği

```
Kullanıcı İsteği: "Dashboard'u olan ve kimlik doğrulama içeren bir Next.js uygulaması yap"

1. İSTEK SINIFLANDIRMA
   ├─ Tip: Yeni özellik inşa et
   ├─ Alan: Frontend + Backend
   ├─ Karmaşıklık: Orta-Yüksek
   └─ Önerilen: /create veya /orchestrate

2. İŞ AKIŞI SEÇİMİ
   └─ Kullanıcı seçimi: /orchestrate (çoklu-ajan yaklaşımı)

3. ORKESTRATÖR KIRILIMI
   ├─ Frontend: Panel Arayüzü (React bileşenleri)
   ├─ Backend: Auth API (JWT, oturum yönetimi)
   ├─ Veritabanı: Kullanıcı şeması (Prisma)
   └─ Test: E2E auth akışı

4. AJAN ATAMASI
   ├─ frontend-specialist
   │   └─ Yetenekler: react-best-practices, tailwind-patterns, frontend-design
   ├─ backend-specialist
   │   └─ Yetenekler: api-patterns, nodejs-best-practices
   ├─ database-architect
   │   └─ Yetenekler: database-design, prisma-expert
   └─ test-engineer
       └─ Yetenekler: testing-patterns, webapp-testing

5. SIRALI ÇOKLU ALAN YÜRÜTME
   Not: YZ her alanı sıralı işler ve uzman "personalar" arasında bağlam değiştirir.
   Bu gerçek bir paralel yürütme değil, simüle edilmiş çoklu ajan davranışıdır.

   ├─ Frontend inşası:
   │   ├─ app/dashboard/page.tsx (Server Component)
   │   ├─ components/DashboardLayout.tsx
   │   ├─ components/LoginForm.tsx
   │   └─ lib/auth-client.ts
   ├─ Backend inşası:
   │   ├─ app/api/auth/login/route.ts
   │   ├─ app/api/auth/logout/route.ts
   │   ├─ lib/jwt.ts
   │   └─ middleware.ts
   ├─ Veritabanı inşası:
   │   ├─ prisma/schema.prisma (Kullanıcı, Oturum modelleri)
   │   └─ prisma/migrations/
   └─ Test inşası:
       ├─ tests/auth.spec.ts (Playwright)
       └─ tests/dashboard.spec.ts

6. KOD ENTEGRASYONU
   Gerçeklik Notu: YZ kodu sürekli bir akış olarak yazar, tutarlılığı korur.
   Bir "merge" adımı yoktur - her şey baştan uyumlu olarak üretilir.

   └─ YZ alanlar arası tutarlılığı korur
       ├─ İçe aktarma (import) yollarını çözer
       ├─ Tip güvenliğini (Type safety) sağlar
       └─ API rotalarını arayüze bağlar

7. DOĞRULAMA
   ├─ checklist.py
   │   ✓ Güvenlik: Sızdırılan gizli bilgi yok
   │   ✓ Lint: ESLint hatası yok
   │   ✓ Tipler: TypeScript başarılı
   │   ✓ Testler: Auth akışı başarılı
   └─ verify_all.py
       ✓ E2E: Giriş → Panel → Çıkış çalışıyor
       ✓ Erişilebilirlik: WCAG AA uyumlu
       ✓ Performans: Lighthouse skoru > 90

8. SONUÇ TESLİMİ
   └─ Kullanıcı şunları alır:
       ├─ Tam kod tabanı
       ├─ Dokümantasyon (nasıl çalıştırılır)
       ├─ Test raporları
       └─ Dağıtım talimatları
```

---

## 📈 İstatistikler & Metrikler

```
┌──────────────────────────────────────────────────────────┐
│                    SİSTEM YETENEKLERİ                     │
├──────────────────────────────────────────────────────────┤
│ Toplam Ajan:               20                            │
│ Toplam Yetenek:            36                            │
│ Toplam İş Akışı:           11                            │
│ Ana Scriptler:             2 (checklist, verify_all)     │
│ Yetenek Düzeyi Scriptler:  18                            │
│ Kapsam:                    ~%90 web/mobil gelişim        │
│                                                          │
│ Desteklenen Framework'ler:                               │
│ ├─ Frontend: React, Next.js, Vue, Nuxt, Astro            │
│ ├─ Backend: Node.js, NestJS, FastAPI, Express            │
│ ├─ Mobil: React Native, Flutter                          │
│ ├─ Veritabanı: Prisma, TypeORM, Sequelize                │
│ ├─ Test: Jest, Vitest, Playwright, Cypress               │
│ └─ DevOps: Docker, Vercel, AWS, GitHub Actions           │
└──────────────────────────────────────────────────────────┘
```

---

## 🎓 En İyi Uygulamalar

### Hangi İş Akışı Ne Zaman Kullanılır?

```
/brainstorm
  ✓ Belirsiz gereksinimler
  ✓ Seçenekleri keşfetme ihtiyacı
  ✓ Karmaşık problemin bölünmesi

/create
  ✓ Mevcut projede yeni özellik
  ✓ Küçük-orta karmaşıklık
  ✓ Tek alan (frontend VEYA backend)

/orchestrate
  ✓ Full-stack özellikler
  ✓ Karmaşık çok adımlı görevler
  ✓ Birden fazla uzman ajana ihtiyaç duyulması

/debug
  ✓ Hata raporları
  ✓ Beklenmedik davranış
  ✓ Performans sorunları

/test
  ✓ Test kapsamı ihtiyacı
  ✓ Dağıtım öncesi
  ✓ Büyük değişikliklerden sonra

/deploy
  ✓ Yayına hazır
  ✓ Tüm testler geçtikten sonra
  ✓ Prodüksiyon URL'sine ihtiyaç var

/plan
  ✓ Büyük projeler
  ✓ Zaman tahminleri gerekliliği
  ✓ Takım koordinasyonu gerekliliği
```

---

## 🔗 Hızlı Referans Bağlantıları

- **Mimari**: `.agent/ARCHITECTURE.md`
- **Ajanlar**: `.agent/agents/`
- **Yetenekler**: `.agent/skills/`
- **İş Akışları**: `.agent/workflows/`
- **Scriptler**: `.agent/scripts/`

---

**Son Güncelleme**: 2026-02-02
**Versiyon**: 2.0.1
