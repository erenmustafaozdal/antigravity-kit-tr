---
name: bash-linux
description: Bash/Linux terminal desenleri. Kritik komutlar, piping, hata yönetimi ve betik yazımı (scripting). macOS veya Linux sistemlerinde çalışırken kullanın.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Bash Linux Desenleri

> Linux/macOS üzerinde Bash kullanımı için temel desenler.

---

## 1. Operatör Sözdizimi

### Komutları Zincirleme

| Operatör | Anlamı | Örnek |
|----------|---------|---------|
| `;` | Sırayla çalıştır | `komut1; komut2` |
| `&&` | İlki başarılıysa çalıştır | `npm install && npm run dev` |
| `\|\|` | İlki başarısızsa çalıştır | `npm test \|\| echo "Testler başarısız"` |
| `\|` | Çıktıyı diğerine aktar (Pipe) | `ls \| grep ".js"` |

---

## 2. Dosya İşlemleri

### Temel Komutlar

| Görev | Komut |
|------|---------|
| Hepsini listele | `ls -la` |
| Dosya bulma | `find . -name "*.js" -type f` |
| Dosya içeriği | `cat dosya.txt` |
| İlk N satır | `head -n 20 dosya.txt` |
| Son N satır | `tail -n 20 dosya.txt` |
| Log takibi | `tail -f log.txt` |
| Dosya içinde ara | `grep -r "desen" --include="*.js"` |
| Dosya boyutu | `du -sh *` |
| Disk kullanımı | `df -h` |

---

## 3. Süreç (Process) Yönetimi

| Görev | Komut |
|------|---------|
| Süreçleri listele | `ps aux` |
| İsme göre bul | `ps aux \| grep node` |
| PID ile durdur | `kill -9 <PID>` |
| Portu kullananı bul | `lsof -i :3000` |
| Portu temizle | `kill -9 $(lsof -t -i :3000)` |
| Arka planda çalıştır | `npm run dev &` |
| İşleri listele | `jobs -l` |
| Ön plana getir | `fg %1` |

---

## 4. Metin İşleme

### Temel Araçlar

| Araç | Amacı | Örnek |
|------|---------|---------|
| `grep` | Arama | `grep -rn "TODO" src/` |
| `sed` | Değiştirme | `sed -i 's/eski/yeni/g' dosya.txt` |
| `awk` | Sütun ayıklama | `awk '{print $1}' dosya.txt` |
| `cut` | Alan kesme | `cut -d',' -f1 veri.csv` |
| `sort` | Sıralama | `sort -u dosya.txt` |
| `uniq` | Benzersiz satırlar | `sort dosya.txt \| uniq -c` |
| `wc` | Sayma | `wc -l dosya.txt` |

---

## 5. Ortam Değişkenleri (Environment Variables)

| Görev | Komut |
|------|---------|
| Hepsini gör | `env` veya `printenv` |
| Birini gör | `echo $PATH` |
| Geçici ata | `export DEGISKEN="değer"` |
| Komutla birlikte ata | `DEGISKEN="değer" komut` |
| PATH'e ekle | `export PATH="$PATH:/yeni/yol"` |

---

## 6. Ağ (Network)

| Görev | Komut |
|------|---------|
| Dosya indir | `curl -O https://örnek.com/dosya` |
| API isteği | `curl -X GET https://api.örnek.com` |
| POST JSON | `curl -X POST -H "Content-Type: application/json" -d '{"anahtar":"değer"}' URL` |
| Port kontrolü | `nc -zv localhost 3000` |
| Ağ bilgileri | `ifconfig` veya `ip addr` |

---

## 7. Betik (Script) Şablonu

```bash
#!/bin/bash
set -euo pipefail  # Hata oluştuğunda, tanımsız değişkende veya pipe hatasında çık

# Renkler (isteğe bağlı)
RED='\033[0;31m'
GREEN='\033[0;32m'
NC='\033[0m'

# Betik dizini
SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"

# Fonksiyonlar
log_info() { echo -e "${GREEN}[BİLGİ]${NC} $1"; }
log_error() { echo -e "${RED}[HATA]${NC} $1" >&2; }

# Ana Bölüm
main() {
    log_info "Başlatılıyor..."
    # Mantık buraya gelecek
    log_info "Tamamlandı!"
}

main "$@"
```

---

## 8. Yaygın Desenler

### Komut varlığını kontrol etme

```bash
if command -v node &> /dev/null; then
    echo "Node yüklü"
fi
```

### Değişkene varsayılan değer atama

```bash
ISIM=${1:-"varsayilan_deger"}
```

### Dosyayı satır satır okuma

```bash
while IFS= read -r line; do
    echo "$line"
done < dosya.txt
```

### Dosyalar üzerinde döngü

```bash
for dosya in *.js; do
    echo "İşleniyor: $dosya"
done
```

---

## 9. PowerShell ile Farklar

| Görev | PowerShell | Bash |
|------|------------|------|
| Dosya listele | `Get-ChildItem` | `ls -la` |
| Dosya bul | `Get-ChildItem -Recurse` | `find . -type f` |
| Ortam Değişkeni | `$env:VAR` | `$VAR` |
| Dize birleştirme | `"$a$b"` | `"$a$b"` (aynı) |
| Null kontrolü | `if ($x)` | `if [ -n "$x" ]` |
| Pipeline | Nesne tabanlı | Metin tabanlı |

---

## 10. Hata Yönetimi

### Seçenekleri belirleme

```bash
set -e          # Hata oluştuğunda dur
set -u          # Tanımsız değişken kullanımında dur
set -o pipefail # Pipe hatalarında dur
set -x          # Hata ayıklama: komutları yazdır
```

### Temizlik için Trap (Tuzak)

```bash
cleanup() {
    echo "Temizlik yapılıyor..."
    rm -f /tmp/gecici_dosya
}
trap cleanup EXIT
```

---

> **Unutmayın:** Bash metin tabanlıdır. Başarı zincirleri için `&&`, güvenlik için `set -e` kullanın ve değişkenlerinizi her zaman tırnak içine alın!
