---
name: systematic-debugging
description: Kök neden analizi ve kanıta dayalı doğrulama ile 4 aşamalı sistematik hata ayıklama metodolojisi. Karmaşık sorunları ayıklarken kullan.
allowed-tools: Read, Glob, Grep
---

# Sistematik Hata Ayıklama (Systematic Debugging)

> Kaynak: obra/superpowers

## Genel Bakış
Bu yetenek, rastgele tahmini önleyen ve sorunları çözmeden önce düzgün anlaşılmasını sağlayan yapılandırılmış bir hata ayıklama yaklaşımı sağlar.

## 4 Aşamalı Hata Ayıklama Süreci

### Aşama 1: Yeniden Üret
Düzeltmeden önce, sorunu güvenilir bir şekilde yeniden üret.

```markdown
## Yeniden Üretme Adımları
1. [Yeniden üretmek için tam adım]
2. [Sonraki adım]
3. [Beklenen vs gerçek sonuç]

## Yeniden Üretme Oranı
- [ ] Her zaman (%100)
- [ ] Sıklıkla (%50-90)
- [ ] Bazen (%10-50)
- [ ] Nadir (%10'dan az)
```

### Aşama 2: İzole Et
Kaynağı daralt.

```markdown
## İzolasyon Soruları
- Bu ne zaman olmaya başladı?
- Son zamanlarda ne değişti?
- Tüm ortamlarda oluyor mu?
- Minimal kodla yeniden üretebilir miyiz?
- Tetikleyen en küçük değişiklik nedir?
```

### Aşama 3: Anla
Sadece belirtileri değil, kök nedeni bul.

```markdown
## Kök Neden Analizi
### 5 Neden (The 5 Whys)
1. Neden: [İlk gözlem]
2. Neden: [Daha derin sebep]
3. Neden: [Hala daha derin]
4. Neden: [Yaklaşıyoruz]
5. Neden: [Kök neden]
```

### Aşama 4: Düzelt & Doğrula
Düzelt ve gerçekten düzeltildiğini doğrula.

```markdown
## Düzeltme Doğrulaması
- [ ] Hata artık yeniden üretilmiyor
- [ ] İlgili işlevsellik hala çalışıyor
- [ ] Yeni bir sorun eklenmedi
- [ ] Regresyonu önlemek için test eklendi
```

## Hata Ayıklama Kontrol Listesi

```markdown
## Başlamadan Önce
- [ ] Tutarlı bir şekilde yeniden üretebilir
- [ ] Minimal yeniden üretme durumuna sahibiz
- [ ] Beklenen davranışı anlıyoruz

## Araştırma Sırasında
- [ ] Son değişiklikleri kontrol et (git log)
- [ ] Hatalar için logları kontrol et
- [ ] Gerekirse loglama ekle
- [ ] Debugger/breakpoint kullan

## Düzeltmeden Sonra
- [ ] Kök neden belgelendi
- [ ] Düzeltme doğrulandı
- [ ] Regresyon testi eklendi
- [ ] Benzer kod kontrol edildi
```

## Yaygın Hata Ayıklama Komutları

```bash
# Son değişiklikler
git log --oneline -20
git diff HEAD~5

# Desen ara
grep -r "errorPattern" --include="*.ts"

# Logları kontrol et
pm2 logs app-name --err --lines 100
```

## Anti-Desenler

❌ **Rastgele değişiklikler** - "Belki bunu değiştirirsem..."
❌ **Kanıtları görmezden gelme** - "Bu neden olamaz"
❌ **Varsayma** - Kanıt olmadan "X olmalı"
❌ **Önce yeniden üretmeme** - Körü körüne düzeltme
❌ **Belirtilerde durma** - Kök nedeni bulmama
