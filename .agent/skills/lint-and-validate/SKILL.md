---
name: lint-and-validate
description: Otomatik kalite kontrolleri, linting ve statik analiz prosedürleri. Her kod değişikliğinden sonra sözdizimi doğruluğunu ve proje standartlarını sağlamak için kullanın. Tetikleme anahtar kelimeleri: lint, format, check, validate, types, static analysis.
allowed-tools: Read, Glob, Grep, Bash
---

# Lint ve Doğrulama Yeteneği (Lint and Validate)

> **ZORUNLU:** Her kod değişikliğinden sonra uygun doğrulama araçlarını çalıştırın. Kod hatasız olana kadar görevi bitirmeyin.

### Ekosisteme Göre Prosedürler

####Node.js / TypeScript
1. **Lint/Düzelt:** `npm run lint` veya `npx eslint "yol" --fix`
2. **Tipler:** `npx tsc --noEmit`
3. **Güvenlik:** `npm audit --audit-level=high`

#### Python
1. **Linter (Ruff):** `ruff check "yol" --fix` (Hızlı ve Modern)
2. **Güvenlik (Bandit):** `bandit -r "yol" -ll`
3. **Tipler (MyPy):** `mypy "yol"`

## Kalite Döngüsü

1. **Kod Yaz/Düzenle**
2. **Denetim Çalıştır:** `npm run lint && npx tsc --noEmit`
3. **Raporu Analiz Et:** "SON DENETİM RAPORU" (FINAL AUDIT REPORT) bölümünü kontrol edin.
4. **Düzelt ve Tekrarla:** "SON DENETİM" hataları ile kod göndermek İZİN VERİLMEZ.

## Hata Yönetimi

- `lint` başarısız olursa: Stil veya sözdizimi sorunlarını hemen düzeltin.
- `tsc` başarısız olursa: Devam etmeden önce tip uyumsuzluklarını düzeltin.
- Araç yapılandırılmamışsa: Proje kökündeki `.eslintrc`, `tsconfig.json`, `pyproject.toml` dosyalarını kontrol edin ve oluşturma önerin.

---

**Katı Kural:** Bu kontrolleri geçmeden hiçbir kod commit edilmemeli veya "tamamlandı" olarak raporlanmamalıdır.

---

## Scriptler

| Script | Amaç | Komut |
|--------|---------|---------|
| `scripts/lint_runner.py` | Birleşik lint kontrolü | `python scripts/lint_runner.py <proje_yolu>` |
| `scripts/type_coverage.py` | Tip kapsama analizi | `python scripts/type_coverage.py <proje_yolu>` |
