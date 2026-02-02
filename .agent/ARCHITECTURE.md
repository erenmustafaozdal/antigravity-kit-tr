# Antigravity Kit Mimarisi

> Kapsamlı YZ Ajan Yetenek Genişletme Araç Kiti

---

## 📋 Genel Bakış

Antigravity Kit, aşağıdaki bileşenlerden oluşan modüler bir sistemdir:

- **20 Uzman Ajan** - Rol tabanlı YZ personaları
- **36 Yetenek** - Alana özgü bilgi modülleri
- **11 İş Akışı** - Slash komut prosedürleri

---

## 🏗️ Dizin Yapısı

```plaintext
.agent/
├── ARCHITECTURE.md          # Bu dosya
├── agents/                  # 20 Uzman Ajan
├── skills/                  # 36 Yetenek
├── workflows/               # 11 Slash Komutları
├── rules/                   # Global Kurallar
└── scripts/                 # Ana Doğrulama Scriptleri
```

---

## 🤖 Ajanlar (20)

Farklı alanlar için uzmanlaşmış YZ personaları.

| Ajan                     | Odak Noktası               | Kullanılan Yetenekler                                    |
| ------------------------ | -------------------------- | -------------------------------------------------------- |
| `orchestrator`           | Çoklu ajan koordinasyonu   | parallel-agents, behavioral-modes                        |
| `project-planner`        | Keşif, görev planlama      | brainstorming, plan-writing, architecture                |
| `frontend-specialist`    | Web UI/UX                  | frontend-design, react-best-practices, tailwind-patterns |
| `backend-specialist`     | API, iş mantığı            | api-patterns, nodejs-best-practices, database-design     |
| `database-architect`     | Şema, SQL                  | database-design, prisma-expert                           |
| `mobile-developer`       | iOS, Android, RN           | mobile-design                                            |
| `game-developer`         | Oyun mantığı, mekanikler   | game-development                                         |
| `devops-engineer`        | CI/CD, Docker              | deployment-procedures, docker-expert                     |
| `security-auditor`       | Güvenlik uyumluluğu        | vulnerability-scanner, red-team-tactics                  |
| `penetration-tester`     | Ofansif güvenlik           | red-team-tactics                                         |
| `test-engineer`          | Test stratejileri          | testing-patterns, tdd-workflow, webapp-testing           |
| `debugger`               | Kök neden analizi          | systematic-debugging                                     |
| `performance-optimizer`  | Hız, Web Vitals            | performance-profiling                                    |
| `seo-specialist`         | Sıralama, görünürlük       | seo-fundamentals, geo-fundamentals                       |
| `documentation-writer`   | Kılavuzlar, dokümanlar     | documentation-templates                                  |
| `product-manager`        | Gereksinimler, kullanıcı hikayeleri | plan-writing, brainstorming                    |
| `product-owner`          | Strateji, backlog, MVP     | plan-writing, brainstorming                              |
| `qa-automation-engineer` | E2E testi, CI pipeline'ları | webapp-testing, testing-patterns                         |
| `code-archaeologist`     | Eski kod, refactoring      | clean-code, code-review-checklist                        |
| `explorer-agent`         | Kod tabanı analizi         | -                                                        |

---

## 🧩 Yetenekler (36)

Ajanların görev bağlamına göre isteğe bağlı olarak yükleyebilecekleri modüler bilgi alanları.

### Frontend & UI

| Yetenek                 | Açıklama                                                              |
| ----------------------- | --------------------------------------------------------------------- |
| `react-best-practices`  | React & Next.js performans optimizasyonu (Vercel - 57 kural)          |
| `web-design-guidelines` | Web UI denetimi - Erişilebilirlik, UX, performans için 100+ kural     |
| `tailwind-patterns`     | Tailwind CSS v4 yardımcı sınıfları                                    |
| `frontend-design`       | UI/UX desenleri, tasarım sistemleri                                   |
| `ui-ux-pro-max`         | 50 stil, 21 palet, 50 font                                            |

### Backend & API

| Yetenek                 | Açıklama                       |
| ----------------------- | ------------------------------ |
| `api-patterns`          | REST, GraphQL, tRPC            |
| `nestjs-expert`         | NestJS modülleri, DI, dekoratörler |
| `nodejs-best-practices` | Node.js asenkron, modüller     |
| `python-patterns`       | Python standartları, FastAPI   |

### Veritabanı

| Yetenek           | Açıklama                    |
| ----------------- | --------------------------- |
| `database-design` | Şema tasarımı, optimizasyon |
| `prisma-expert`   | Prisma ORM, migrasyonlar    |

### TypeScript/JavaScript

| Yetenek             | Açıklama                            |
| ------------------- | ----------------------------------- |
| `typescript-expert` | Tip seviyesinde programlama, performans |

### Bulut & Altyapı

| Yetenek                 | Açıklama                  |
| ----------------------- | ------------------------- |
| `docker-expert`         | Konteynerizasyon, Compose |
| `deployment-procedures` | CI/CD, dağıtım iş akışları |
| `server-management`     | Altyapı yönetimi          |

### Test & Kalite

| Yetenek                 | Açıklama                 |
| ----------------------- | ------------------------ |
| `testing-patterns`      | Jest, Vitest, stratejiler |
| `webapp-testing`        | E2E, Playwright          |
| `tdd-workflow`          | Test güdümlü geliştirme  |
| `code-review-checklist` | Kod inceleme standartları |
| `lint-and-validate`     | Linting, doğrulama       |

### Güvenlik

| Yetenek                 | Açıklama                 |
| ----------------------- | ------------------------ |
| `vulnerability-scanner` | Güvenlik denetimi, OWASP |
| `red-team-tactics`      | Ofansif güvenlik         |

### Mimari & Planlama

| Yetenek         | Açıklama                    |
| --------------- | --------------------------- |
| `app-builder`   | Full-stack uygulama iskeleti |
| `architecture`  | Sistem tasarım desenleri    |
| `plan-writing`  | Görev planlama, kırılım     |
| `brainstorming` | Sokratik sorgulama          |

### Mobil

| Yetenek         | Açıklama              |
| --------------- | --------------------- |
| `mobile-design` | Mobil UI/UX desenleri |

### Oyun Geliştirme

| Yetenek            | Açıklama                |
| ------------------ | ----------------------- |
| `game-development` | Oyun mantığı, mekanikler |

### SEO & Büyüme

| Yetenek            | Açıklama                      |
| ------------------ | ----------------------------- |
| `seo-fundamentals` | SEO, E-E-A-T, Core Web Vitals |
| `geo-fundamentals` | GenAI optimizasyonu           |

### Shell/CLI

| Yetenek              | Açıklama                  |
| -------------------- | ------------------------- |
| `bash-linux`         | Linux komutları, scripting |
| `powershell-windows` | Windows PowerShell        |

### Diğerleri

| Yetenek                   | Açıklama                  |
| ------------------------- | ------------------------- |
| `clean-code`              | Kodlama standartları (Global) |
| `behavioral-modes`        | Ajan personaları          |
| `parallel-agents`         | Çoklu ajan desenleri      |
| `mcp-builder`             | Model Context Protocol    |
| `documentation-templates` | Doküman formatları        |
| `i18n-localization`       | Uluslararasılaştırma      |
| `performance-profiling`   | Web Vitals, optimizasyon  |
| `systematic-debugging`    | Sorun giderme             |

---

## 🔄 İş Akışları (11)

Slash komut prosedürleri. `/komut` ile çağrılır.

| Komut            | Açıklama                 |
| ---------------- | ------------------------ |
| `/brainstorm`    | Sokratik keşif           |
| `/create`        | Yeni özellikler oluşturma |
| `/debug`         | Sorun giderme            |
| `/deploy`        | Uygulama dağıtımı        |
| `/enhance`       | Mevcut kodu iyileştirme  |
| `/orchestrate`   | Çoklu ajan koordinasyonu |
| `/plan`          | Görev kırılımı           |
| `/preview`       | Değişiklikleri önizleme  |
| `/status`        | Proje durumunu kontrol et |
| `/test`          | Testleri çalıştır        |
| `/ui-ux-pro-max` | 50 stil ile tasarım      |

---

## 🎯 Yetenek Yükleme Protokolü

```plaintext
Kullanıcı İsteği → Yetenek Açıklaması Eşleşmesi → SKILL.md Yükle
                                             ↓
                                     references/ Oku
                                             ↓
                                     scripts/ Oku
```

### Yetenek Yapısı

```plaintext
yetenek-adi/
├── SKILL.md           # (Zorunlu) Metaveri ve talimatlar
├── scripts/           # (Opsiyonel) Python/Bash scriptleri
├── references/        # (Opsiyonel) Şablonlar, dokümanlar
└── assets/            # (Opsiyonel) Görseller, logolar
```

### Gelişmiş Yetenekler (scripts/references ile)

| Yetenek             | Dosyalar | Kapsam                              |
| ------------------- | -------- | ----------------------------------- |
| `ui-ux-pro-max`     | 27       | 50 stil, 21 palet, 50 font          |
| `app-builder`       | 20       | Full-stack yapı kurma               |

---

## ⚙️ Scriptler (2)

Yetenek seviyesindeki scriptleri koordine eden ana doğrulama scriptleri.

### Ana Scriptler

| Script          | Amaç                                    | Ne Zaman Kullanılır      |
| --------------- | --------------------------------------- | ------------------------ |
| `checklist.py`  | Öncelik tabanlı doğrulama (Temel)       | Geliştirme, pre-commit   |
| `verify_all.py` | Kapsamlı doğrulama (Tüm kontroller)     | Dağıtım öncesi, sürümler |

### Kullanım

```bash
# Geliştirme sırasında hızlı doğrulama
python .agent/scripts/checklist.py .

# Dağıtım öncesi tam doğrulama
python .agent/scripts/verify_all.py . --url http://localhost:3000
```

### Neleri Kontrol Ederler?

**checklist.py** (Temel kontroller):

- Güvenlik (zafiyetler, sırlar)
- Kod Kalitesi (lint, tipler)
- Şema Doğrulama
- Test Paketi
- UX Denetimi
- SEO Kontrolü

**verify_all.py** (Tam paket):

- checklist.py içindeki her şey ARTI:
- Lighthouse (Core Web Vitals)
- Playwright E2E
- Paket Analizi (Bundle Analysis)
- Mobil Denetim
- i18n Kontrolü

Detaylar için bkz. [scripts/README.md](scripts/README.md)

---

## 📊 İstatistikler

| Metrik             | Değer                         |
| ------------------ | ----------------------------- |
| **Toplam Ajan**    | 20                            |
| **Toplam Yetenek** | 36                            |
| **Toplam İş Akışı**| 11                            |
| **Toplam Script**  | 2 (ana) + 18 (yetenek bazlı)  |
| **Kapsam**         | ~%90 web/mobil geliştirme     |

---

## 🔗 Hızlı Referans

| İhtiyaç   | Ajan                  | Yetenekler                            |
| --------- | --------------------- | ------------------------------------- |
| Web Uyg.  | `frontend-specialist` | react-best-practices, frontend-design |
| API       | `backend-specialist`  | api-patterns, nodejs-best-practices   |
| Mobil     | `mobile-developer`    | mobile-design                         |
| Veritabanı| `database-architect`  | database-design, prisma-expert        |
| Güvenlik  | `security-auditor`    | vulnerability-scanner                 |
| Test      | `test-engineer`       | testing-patterns, webapp-testing      |
| Hata Giderme | `debugger`         | systematic-debugging                  |
| Plan      | `project-planner`     | brainstorming, plan-writing           |
