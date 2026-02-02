---
name: powershell-windows
description: PowerShell Windows desenleri. Kritik tuzaklar, operatör sözdizimi, hata yönetimi.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# PowerShell Windows Desenleri

> Windows PowerShell için kritik desenler ve tuzaklar.

---

## 1. Operatör Sözdizimi Kuralları

### KRİTİK: Parantez Gerekli

| ❌ Yanlış | ✅ Doğru |
|----------|----------|
| `if (Test-Path "a" -or Test-Path "b")` | `if ((Test-Path "a") -or (Test-Path "b"))` |
| `if (Get-Item $x -and $y -eq 5)` | `if ((Get-Item $x) -and ($y -eq 5))` |

**Kural:** Mantıksal operatörler kullanılırken her cmdlet çağrısı parantez içinde olmalıdır.

---

## 2. Unicode/Emoji Kısıtlaması

### KRİTİK: Script'lerde Unicode Yok

| Amaç | ❌ Kullanma | ✅ Kullan |
|------|-------------|-----------|
| Başarı | ✅ ✓ | [OK] [+] |
| Hata | ❌ ✗ 🔴 | [!] [X] |
| Uyarı | ⚠️ 🟡 | [*] [WARN] |
| Bilgi | ℹ️ 🔵 | [i] [INFO] |
| İlerleme | ⏳ | [...] |

**Kural:** PowerShell script'lerinde yalnızca ASCII karakterler kullanın.

---

## 3. Null Kontrolü Desenleri

### Erişimden Önce Her Zaman Kontrol Et

| ❌ Yanlış | ✅ Doğru |
|----------|----------|
| `$array.Count -gt 0` | `$array -and $array.Count -gt 0` |
| `$text.Length` | `if ($text) { $text.Length }` |

---

## 4. String İnterpolasyonu

### Karmaşık İfadeler

| ❌ Yanlış | ✅ Doğru |
|----------|----------|
| `"Değer: $($obj.prop.sub)"` | Önce değişkende sakla |

**Desen:**
```
$value = $obj.prop.sub
Write-Output "Değer: $value"
```

---

## 5. Hata Yönetimi

### ErrorActionPreference

| Değer | Kullanım |
|-------|----------|
| Stop | Geliştirme (hızlı başarısız) |
| Continue | Prodüksiyon script'leri |
| SilentlyContinue | Hatalar beklendiğinde |

### Try/Catch Deseni

- Try bloğu içinde return yapma
- Temizleme için finally kullan
- Try/catch'ten sonra return yap

---

## 6. Dosya Yolları

### Windows Yol Kuralları

| Desen | Kullanım |
|-------|----------|
| Literal yol | `C:\Users\User\file.txt` |
| Değişken yol | `Join-Path $env:USERPROFILE "file.txt"` |
| Göreceli | `Join-Path $ScriptDir "data"` |

**Kural:** Platformlar arası güvenlik için Join-Path kullanın.

---

## 7. Dizi İşlemleri

### Doğru Desenler

| İşlem | Sözdizimi |
|-------|-----------|
| Boş dizi | `$array = @()` |
| Öğe ekle | `$array += $item` |
| ArrayList ekle | `$list.Add($item) | Out-Null` |

---

## 8. JSON İşlemleri

### KRİTİK: Depth Parametresi

| ❌ Yanlış | ✅ Doğru |
|----------|----------|
| `ConvertTo-Json` | `ConvertTo-Json -Depth 10` |

**Kural:** İç içe nesneler için her zaman `-Depth` belirtin.

### Dosya İşlemleri

| İşlem | Desen |
|-------|-------|
| Oku | `Get-Content "file.json" -Raw | ConvertFrom-Json` |
| Yaz | `$data | ConvertTo-Json -Depth 10 | Out-File "file.json" -Encoding UTF8` |

---

## 9. Yaygın Hatalar

| Hata Mesajı | Neden | Düzeltme |
|-------------|-------|----------|
| "parameter 'or'" | Eksik parantez | Cmdlet'leri () içine alın |
| "Unexpected token" | Unicode karakter | Yalnızca ASCII kullanın |
| "Cannot find property" | Null nesne | Önce null'u kontrol edin |
| "Cannot convert" | Tip uyuşmazlığı | .ToString() kullanın |

---

## 10. Script Şablonu

```powershell
# Strict mode
Set-StrictMode -Version Latest
$ErrorActionPreference = "Continue"

# Yollar
$ScriptDir = Split-Path -Parent $MyInvocation.MyCommand.Path

# Ana
try {
    # Mantık burada
    Write-Output "[OK] Tamamlandı"
    exit 0
}
catch {
    Write-Warning "Hata: $_"
    exit 1
}
```

---

> **Unutma:** PowerShell'in kendine özgü sözdizimi kuralları vardır. Parantezler, yalnızca ASCII ve null kontrolleri pazarlık konusu değildir.
