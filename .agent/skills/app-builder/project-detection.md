# Proje Türü Tespiti (Project Type Detection)

> Proje türünü ve şablonunu belirlemek için kullanıcı isteklerini analiz eder.

## Anahtar Kelime Matrisi

| Anahtar Kelimeler (TR/EN) | Proje Türü | Şablon |
|----------|--------------|----------|
| blog, yazı, makale, article | Blog | astro-static |
| e-ticaret, e-commerce, ürün, sepet, ödeme | E-ticaret | nextjs-saas |
| dashboard, panel, yönetim, yönetici | Yönetim Paneli | nextjs-fullstack |
| api, backend, servis, rest | API Servisi | express-api |
| python, fastapi, django | Python API | python-fastapi |
| mobil, android, ios, react native | Mobil Uygulama (RN) | react-native-app |
| flutter, dart | Mobil Uygulama (Flutter) | flutter-app |
| portfolyo, portfolio, kişisel, cv | Portfolyo | nextjs-static |
| crm, müşteri, satış, customer | CRM | nextjs-fullstack |
| saas, abonelik, subscription, stripe | SaaS | nextjs-saas |
| landing, açılış sayfası, tanıtım, pazarlama | Landing Page | nextjs-static |
| döküman, docs, dokümantasyon | Dokümantasyon | astro-static |
| eklenti, extension, plugin, chrome | Tarayıcı Eklentisi | chrome-extension |
| masaüstü, desktop, electron | Masaüstü Uygulaması | electron-desktop |
| cli, komut satırı, terminal | CLI Aracı | cli-tool |
| monorepo, workspace | Monorepo | monorepo-turborepo |

## Tespit Süreci

```
1. Kullanıcı isteğini parçalara ayır
2. Anahtar kelimeleri çıkar
3. Proje türünü belirle
4. Eksik bilgileri tespit et → conversation-manager'a yönlendir
5. Teknoloji yığını öner
```
