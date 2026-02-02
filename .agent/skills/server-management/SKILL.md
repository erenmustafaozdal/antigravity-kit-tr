---
name: server-management
description: Sunucu yönetimi prensipleri ve karar verme. Süreç yönetimi, izleme stratejisi ve ölçekleme kararları. Düşünmeyi öğretir, komutları değil.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Sunucu Yönetimi (Server Management)

> Prodüksiyon işlemleri için sunucu yönetimi prensipleri.
> **Komutları ezberlemek yerine DÜŞÜNMEYİ öğren.**

---

## 1. Süreç Yönetimi Prensipleri

### Araç Seçimi

| Senaryo | Araç |
|---------|------|
| **Node.js uygulaması** | PM2 (clustering, reload) |
| **Herhangi bir uygulama** | systemd (Linux native) |
| **Container'lar** | Docker/Podman |
| **Orkestrasyon** | Kubernetes, Docker Swarm |

### Süreç Yönetimi Hedefleri

| Hedef | Anlamı |
|-------|--------|
| **Çökmede yeniden başlat** | Otomatik kurtarma |
| **Sıfır kesinti reload** | Servis kesintisi yok |
| **Clustering** | Tüm CPU çekirdeklerini kullan |
| **Kalıcılık** | Sunucu yeniden başlatmayı atlatır |

---

## 2. İzleme Prensipleri

### Neyi İzlemeli

| Kategori | Anahtar Metrikler |
|----------|-------------------|
| **Erişilebilirlik** | Uptime, health check'ler |
| **Performans** | Yanıt süresi, throughput |
| **Hatalar** | Hata oranı, tipler |
| **Kaynaklar** | CPU, bellek, disk |

### Alarm Önem Stratejisi

| Seviye | Yanıt |
|--------|-------|
| **Kritik** | Hemen aksiyon |
| **Uyarı** | Yakında araştır |
| **Bilgi** | Günlük incele |

### İzleme Aracı Seçimi

| İhtiyaç | Seçenekler |
|---------|------------|
| Basit/Ücretsiz | PM2 metrikleri, htop |
| Tam gözlemlenebilirlik | Grafana, Datadog |
| Hata izleme | Sentry |
| Uptime | UptimeRobot, Pingdom |

---

## 3. Log Yönetimi Prensipleri

### Log Stratejisi

| Log Tipi | Amaç |
|----------|------|
| **Uygulama logları** | Debug, denetim |
| **Erişim logları** | Trafik analizi |
| **Hata logları** | Sorun tespiti |

### Log Prensipleri

1. **Logları rotate et** disk dolmasını önlemek için
2. **Yapılandırılmış loglama** (JSON) parsing için
3. **Uygun seviyeler** (error/warn/info/debug)
4. **Hassas veri yok** loglarda

---

## 4. Ölçekleme Kararları

### Ne Zaman Ölçeklemeli

| Belirti | Çözüm |
|---------|-------|
| Yüksek CPU | Instance ekle (horizontal) |
| Yüksek bellek | RAM artır veya sızıntıyı düzelt |
| Yavaş yanıt | Önce profillle, sonra ölçekle |
| Trafik artışları | Otomatik ölçekleme |

### Ölçekleme Stratejisi

| Tip | Ne Zaman Kullanılır |
|-----|---------------------|
| **Dikey** | Hızlı düzeltme, tek instance |
| **Yatay** | Sürdürülebilir, dağıtık |
| **Otomatik** | Değişken trafik |

---

## 5. Health Check Prensipleri

### Neyi Sağlıklı Yapar

| Kontrol | Anlam |
|---------|-------|
| **HTTP 200** | Servis yanıt veriyor |
| **Veritabanı bağlı** | Veriye erişilebilir |
| **Bağımlılıklar OK** | Harici servislere ulaşılıyor |
| **Kaynaklar OK** | CPU/bellek tükenmedi |

### Health Check İmplementasyonu

- Basit: Sadece 200 döndür
- Derin: Tüm bağımlılıkları kontrol et
- Load balancer ihtiyaçlarına göre seç

---

## 6. Güvenlik Prensipleri

| Alan | Prensip |
|------|---------|
| **Erişim** | Yalnızca SSH anahtarları, şifre yok |
| **Firewall** | Yalnızca gerekli portlar açık |
| **Güncellemeler** | Düzenli güvenlik yamaları |
| **Sırlar** | Ortam değişkenleri, dosya değil |
| **Denetim** | Erişimi ve değişiklikleri logla |

---

## 7. Sorun Giderme Önceliği

Bir şeyler ters gittiğinde:

1. **Çalışıyor mu kontrol et** (process durumu)
2. **Logları kontrol et** (hata mesajları)
3. **Kaynakları kontrol et** (disk, bellek, CPU)
4. **Ağı kontrol et** (portlar, DNS)
5. **Bağımlılıkları kontrol et** (veritabanı, API'ler)

---

## 8. Anti-Desenler

| ❌ Yapma | ✅ Yap |
|----------|--------|
| Root olarak çalıştır | Root olmayan kullanıcı kullan |
| Logları görmezden gel | Log rotation kur |
| İzlemeyi atla | İlk günden izle |
| Manuel yeniden başlatma | Otomatik yeniden başlatma yapılandır |
| Yedekleme yok | Düzenli yedekleme takvimi |

---

> **Unutma:** İyi yönetilen bir sunucu sıkıcıdır. Hedef budur.
