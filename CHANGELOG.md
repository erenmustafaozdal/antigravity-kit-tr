# Değişiklik Günlüğü (Changelog)

Antigravity Kit üzerinde yapılan tüm önemli değişiklikler bu dosyada belgelenecektir.

Biçim [Keep a Changelog](https://keepachangelog.com/en/2.0.0/) standardına dayanmaktadır
ve bu proje [Semantik Versiyonlama](https://semver.org/spec/v2.0.0.html) kurallarına uyar.

## [Yayınlanmamış]

## [2.0.1] - 2026-01-26

### Eklendi

- **Ajan Akış Dokümantasyonu**: Yeni kapsamlı iş akışı dokümantasyonu
    - `.agent/AGENT_FLOW.md` eklendi - Tam ajan akış mimarisi rehberi
    - Ajan Yönlendirme Kontrol Listesi eklendi (kod/tasarım işinden önce zorunlu adımlar)
    - Gereksinim netleştirme için Sokratik Kapı Protokolü eklendi
    - Çapraz-Yetenek Referansları deseni dokümante edildi
- **Yeni Yetenekler**:
    - `react-best-practices` - Next.js ve React uzmanlığı birleştirildi
    - `web-design-guidelines` - Profesyonel web tasarım standartları ve desenleri

### Değiştirildi

- **Yetenek Birleştirme**: `nextjs-best-practices` ve `react-patterns`, birleşik `react-best-practices` yeteneği altında toplandı
- **Mimari Güncellemeleri**:
    - `.agent/ARCHITECTURE.md` geliştirilmiş akış diyagramları ile güçlendirildi
    - `.agent/rules/GEMINI.md` Ajan Yönlendirme Kontrol Listesi ile güncellendi
- **Ajan Güncellemeleri**:
    - `frontend-specialist.md` yeni yetenek referansları ile güncellendi
    - `qa-automation-engineer.md` geliştirilmiş test iş akışları ile güncellendi
- **Frontend Tasarım Yeteneği**: `frontend-design/SKILL.md`, `web-design-guidelines` ile çapraz referanslı hale getirildi

### Kaldırıldı

- `nextjs-best-practices` yeteneği kullanımdan kaldırıldı (`react-best-practices` içine dahil edildi)
- `react-patterns` yeteneği kullanımdan kaldırıldı (`react-best-practices` içine dahil edildi)

### Düzeltildi

- **Ajan Akış Doğruluğu**: AGENT_FLOW.md içindeki yanıltıcı terminoloji düzeltildi
    - "Paralel Yürütme" → "Sıralı Çoklu-Alan Yürütme" olarak değiştirildi
    - "Entegrasyon Katmanı" → "Kod Tutarlılığı" olarak doğru açıklamayla değiştirildi
    - YZ'nin sıralı işlemesi vs. simüle edilmiş çoklu-ajan davranışı hakkında gerçekçi notlar eklendi
    - Scriptlerin otomatik çalıştırılmadığı, kullanıcı onayı gerektirdiği netleştirildi

## [2.0.0] - Yayınlanmamış

### İlk Sürüm

- Antigravity Kit ilk sürümü
- 20 özelleşmiş YZ ajanı
- 37 alan-bazlı yetenek
- 11 iş akışı slash komutu
- Kolay kurulum ve güncelleme için CLI aracı
- Kapsamlı dokümantasyon ve mimari rehberi

[Yayınlanmamış]: https://github.com/vudovn/antigravity-kit/compare/v2.0.0...HEAD
[2.0.0]: https://github.com/vudovn/antigravity-kit/releases/tag/v2.0.0
