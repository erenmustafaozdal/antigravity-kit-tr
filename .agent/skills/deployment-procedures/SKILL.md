---
name: deployment-procedures
description: Prodüksiyon dağıtım (deployment) prensipleri ve karar verme. Güvenli dağıtım iş akışları, geri alma (rollback) stratejileri ve doğrulama. Script ezberlemeyi değil, düşünmeyi öğretir.
allowed-tools: Read, Glob, Grep, Bash
---

# Dağıtım Prosedürleri (Deployment Procedures)

> Güvenli prodüksiyon yayınları için dağıtım prensipleri ve karar verme süreçleri.
> **Scriptleri ezberlemeyi değil, DÜŞÜNMEYİ öğrenin.**

---

## ⚠️ Bu Yetenek Nasıl Kullanılır?

Bu yetenek kopyalanacak bash scriptlerini değil, **dağıtım prensiplerini** öğretir.

- Her dağıtım süreci kendine hastır.
- Her adımın arkasındaki "NEDEN"i anlayın.
- Prosedürleri kullandığınız platforma göre uyarlayın.

---

## 1. Platform Seçimi

### Karar Ağacı

```
Ne dağıtıyorsunuz?
│
├── Statik site / JAMstack
│   └── Vercel, Netlify, Cloudflare Pages
│
├── Basit web uygulaması
│   ├── Yönetilen (Managed) → Railway, Render, Fly.io
│   └── Kontrol bizde olsun → VPS + PM2/Docker
│
├── Mikroservisler
│   └── Konteyner orkestrasyonu (Kubernetes vb.)
│
└── Sunucusuz (Serverless)
    └── Edge functions, Lambda
```

### Her Platformun Prosedürü Farklıdır

| Platform | Dağıtım Yöntemi |
|----------|------------------|
| **Vercel/Netlify** | Git push, otomatik dağıtım |
| **Railway/Render** | Git push veya CLI |
| **VPS + PM2** | SSH + manuel adımlar |
| **Docker** | İmaj push + orkestrasyon |
| **Kubernetes** | kubectl apply |

---

## 2. Dağıtım Öncesi Prensipler

### 4 Temel Doğrulama Kategorisi

| Kategori | Neler Kontrol Edilmeli? |
|----------|--------------|
| **Kod Kalitesi** | Testler geçiyor mu, lint temiz mi, inceleme yapıldı mı? |
| **Build** | Prodüksiyon build'i çalışıyor mu, uyarı var mı? |
| **Ortam (Env)** | Port değişkenleri ayarlı mı, secret'lar güncel mi? |
| **Güvenlik** | Yedek alındı mı, geri alma planı hazır mı? |

### Dağıtım Öncesi Kontrol Listesi

- [ ] Tüm testler geçiyor
- [ ] Kod incelendi ve onaylandı
- [ ] Prodüksiyon build'i başarılı
- [ ] Ortam değişkenleri (Env vars) doğrulandı
- [ ] Veritabanı migrasyonları hazır (varsa)
- [ ] Geri alma (rollback) planı dökümante edildi
- [ ] Ekip bilgilendirildi
- [ ] İzleme (monitoring) sistemleri hazır

---

## 3. Dağıtım İş Akışı Prensipleri

### 5 Aşamalı Süreç

```
1. HAZIRLIK (PREPARE)
   └── Kodu, build'i ve env değişkenlerini doğrula

2. YEDEKLEME (BACKUP)
   └── Değişiklikten önce mevcut durumu kaydet

3. DAĞITIM (DEPLOY)
   └── İzleme panelleri açıkken yürüt

4. DOĞRULAMA (VERIFY)
   └── Sağlık kontrolü, loglar ve kritik akışlar

5. ONAYLA veya GERİ AL (CONFIRM or ROLLBACK)
   └── Her şey yolunda mı? Onayla. Sorun mu var? Geri al.
```

### Aşama Prensipleri

| Aşama | Prensip |
|-------|-----------|
| **Hazırlık** | Test edilmemiş kodu asla dağıtma |
| **Yedekleme** | Yedek olmadan geri alma yapılamaz |
| **Dağıtım** | Süreci izleyin, başından ayrılmayın |
| **Doğrulama** | Güvenin ama kontrol edin |
| **Onayla** | Geri alma tetikleyicisi her an hazır olsun |

---

## 4. Dağıtım Sonrası Doğrulama

### Neler Doğrulanmalı?

| Kontrol | Neden? |
|-------|-----|
| **Sağlık (Health) Uç Noktası** | Servis çalışıyor mu? |
| **Hata Logları** | Yeni ve beklenmedik hatalar var mı? |
| **Kritik Akışlar** | Temel özellikler çalışıyor mu? |
| **Performans** | Yanıt süreleri kabul edilebilir mi? |

### Doğrulama Penceresi

- **İlk 5 dakika**: Aktif izleme
- **15 dakika**: Kararlılık onayı
- **1 saat**: Son doğrulama
- **Ertesi gün**: Metriklerin gözden geçirilmesi

---

## 5. Geri Alma (Rollback) Prensipleri

### Ne Zaman Geri Alınmalı?

| Belirti | Eylem |
|---------|--------|
| Servis kapalıysa | Derhal geri al |
| Kritik hatalar varsa | Geri al |
| Performans >%50 düştüyse | Geri almayı değerlendir |
| Küçük sorunlar | Hızlıca düzeltilebiliyorsa devam et |

### Platforma Göre Geri Alma Stratejisi

| Platform | Geri Alma Yöntemi |
|----------|----------------|
| **Vercel/Netlify** | Önceki başarılı commit'i tekrar dağıt |
| **Railway/Render** | Panel üzerinden "Rollback" yap |
| **VPS + PM2** | Yedeği geri yükle, servisi yeniden başlat |
| **Docker** | Önceki imaj etiketine (tag) dön |
| **K8s** | kubectl rollout undo |

### Geri Alma Prensipleri

1. **Hız kusursuzluktan önce gelir**: Önce geri al, sonra hata ayıkla (debug)
2. **Hataları katlamayın**: Tek bir geri alma işlemi yapın, üst üste değişiklik yapmayın
3. **İletişim**: Ekibe ne olduğunu bildirin
4. **Post-mortem**: Sistem kararlı hale geldikten sonra nedenini analiz edin

---

## 6. Sıfır Kesintili Dağıtım (Zero-Downtime)

### Stratejiler

| Strateji | Nasıl Çalışır? |
|----------|--------------|
| **Rolling** | Örnekleri (instances) tek tek değiştirir |
| **Blue-Green** | Trafiği iki ortam arasında değiştirir |
| **Canary** | Trafiği kademeli olarak yeni sürüme aktarır |

### Seçim Prensipleri

| Senaryo | Strateji |
|----------|----------|
| Standart yayın | Rolling |
| Yüksek riskli değişiklik | Blue-green (kolay geri alma) |
| Doğrulama ihtiyacı | Canary (gerçek trafikle test) |

---

## 7. Acil Durum Prosedürleri

### Servis Kesintisi Önceliği

1. **Değerlendir**: Belirti nedir?
2. **Hızlı Düzeltme**: Net değilse yeniden başlatmayı dene
3. **Geri Al**: Yeniden başlatma işe yaramazsa geri al
4. **Araştır**: Sistem kararlı olduktan sonra incele

### İnceleme Sırası

| Kontrol | Yaygın Sorunlar |
|-------|--------------|
| **Loglar** | Hatalar, exception'lar |
| **Kaynaklar** | Dolu disk, bellek (RAM) yetersizliği |
| **Ağ** | DNS sorunları, firewall engelleri |
| **Bağımlılıklar** | Veritabanı veya API bağlantı sorunları |

---

## 8. Anti-Desenler (Kaçınılması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Cuma günü dağıtım yapmak | Haftanın erken günlerinde yapın |
| Aceleyle dağıtım yapmak | Süreci takip edin |
| Staging ortamını atlamak | Her zaman önce test edin |
| Yedek almadan dağıtmak | Dağıtımdan önce mutlaka yedek alın |
| Dağıtımdan sonra ayrılmak | En az 15 dakika izleyin |
| Aynı anda çok fazla değişiklik yapmak | Her seferinde tek bir değişiklik yapın |

---

## 9. Karar Kontrol Listesi

Dağıtımdan önce:

- [ ] **Platforma uygun prosedür seçildi mi?**
- [ ] **Yedekleme stratejisi hazır mı?**
- [ ] **Geri alma planı dökümante edildi mi?**
- [ ] **İzleme (monitoring) yapılandırıldı mı?**
- [ ] **Ekip bilgilendirildi mi?**
- [ ] **Sonrasında izleme için zaman ayrıldı mı?**

---

## 10. En İyi Pratikler

1. Büyük yayınlar yerine **küçük ve sık dağıtımlar** yapın.
2. Riskli değişiklikler için **Feature Flag** (özellik bayrakları) kullanın.
3. Tekrarlayan adımları **otomatize** edin.
4. Her dağıtımı **kayıt altına (dökümante)** alın.
5. Sorunlardan sonra neyin yanlış gittiğini **analiz edin**.
6. Geri almayı, ihtiyacınız olmadan önce **test edin**.

---

> **Unutmayın:** Her dağıtım bir risktir. Riski hızla değil, hazırlıkla minimize edin.
