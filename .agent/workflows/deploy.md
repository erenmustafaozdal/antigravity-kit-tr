---
description: Üretim (production) sürümleri için dağıtım komutu. Dağıtım öncesi kontrolleri ve dağıtım işlemini gerçekleştirir.
---

# /deploy - Üretim Dağıtımı

$ARGUMENTS

---

## Amaç

Bu komut; dağıtım öncesi kontroller, dağıtımın yürütülmesi ve doğrulama aşamalarıyla birlikte üretim ortamına dağıtımı yönetir.

---

## Alt Komutlar

```
/deploy            - Etkileşimli dağıtım sihirbazı
/deploy check      - Sadece dağıtım öncesi kontrolleri çalıştır
/deploy preview    - Önizleme/hazırlık (staging) ortamına dağıt
/deploy production - Üretime (production) dağıt
/deploy rollback   - Önceki sürüme geri dön
```

---

## Dağıtım Öncesi Kontrol Listesi

Herhangi bir dağıtımdan önce:

```markdown
## 🚀 Dağıtım Öncesi Kontrol Listesi

### Kod Kalitesi
- [ ] TypeScript hatası yok (`npx tsc --noEmit`)
- [ ] ESLint geçiyor (`npx eslint .`)
- [ ] Tüm testler geçiyor (`npm test`)

### Güvenlik
- [ ] Hardcoded (açık kodlanmış) gizli bilgi yok
- [ ] Ortam değişkenleri dokümante edildi
- [ ] Bağımlılıklar denetlendi (`npm audit`)

### Performans
- [ ] Paket boyutu kabul edilebilir düzeyde
- [ ] console.log ifadeleri yok
- [ ] Görseller optimize edildi

### Dokümantasyon
- [ ] README güncellendi
- [ ] CHANGELOG güncellendi
- [ ] API dokümanları güncel

### Dağıtıma hazır mısınız? (e/h)
```

---

## Dağıtım Akışı

```
┌─────────────────┐
│  /deploy        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Uçuş öncesi    │
│  kontroller     │
└────────┬────────┘
         │
    Geçti mi? ──Hayır──► Sorunları düzelt
         │
        Evet
         │
         ▼
┌─────────────────┐
│  Uygulama       │
│  Build          │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Platforma      │
│  Dağıtım        │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Sağlık kontrolü│
│  & Doğrulama    │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  ✅ Tamamlandı  │
└─────────────────┘
```

---

## Çıktı Formatı

### Başarılı Dağıtım

```markdown
## 🚀 Dağıtım Tamamlandı

### Özet
- **Sürüm:** v1.2.3
- **Ortam:** production
- **Süre:** 47 saniye
- **Platform:** Vercel

### URL'ler
- 🌐 Üretim: https://app.example.com
- 📊 Dashboard: https://vercel.com/project

### Neler Değişti
- Kullanıcı profili özelliği eklendi
- Giriş hatası düzeltildi
- Bağımlılıklar güncellendi

### Sağlık Kontrolü
✅ API yanıt veriyor (200 OK)
✅ Veritabanı bağlandı
✅ Tüm servisler sağlıklı
```

### Hatalı Dağıtım

```markdown
## ❌ Dağıtım Başarısız

### Hata
Build aşamasında hata oluştu: TypeScript derlemesi

### Detaylar
```
error TS2345: Argument of type 'string' is not assignable...
```

### Çözüm
1. `src/services/user.ts:45` adresindeki TypeScript hatasını düzelt
2. Doğrulamak için yerelde `npm run build` çalıştır
3. Tekrar `/deploy` yapmayı dene

### Geri Dönüş (Rollback) Mevcut
Önceki sürüm (v1.2.2) hala aktif.
Gerekirse `/deploy rollback` komutunu çalıştırın.
```

---

## Platform Desteği

| Platform | Komut | Notlar |
|----------|---------|-------|
| Vercel | `vercel --prod` | Next.js için otomatik algılanır |
| Railway | `railway up` | Railway CLI gerektirir |
| Fly.io | `fly deploy` | flyctl gerektirir |
| Docker | `docker compose up -d` | Self-hosted için |

---

## Örnekler

```
/deploy
/deploy check
/deploy preview
/deploy production --skip-tests
/deploy rollback
```
