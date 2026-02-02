# Mobil Backend Desenleri

> **Bu dosya, mobil istemcilere ÖZEL backend/API desenlerini kapsar.**
> Genel backend desenleri `nodejs-best-practices` ve `api-patterns` dosyalarındadır.
> **Mobil backend, web backend ile aynı değildir. Farklı kısıtlamalar, farklı desenler.**

---

## 🧠 MOBİL BACKEND ZİHNİYETİ

```
Mobil istemciler web istemcilerinden FARKLI özelliklere sahiptir:
├── Güvenilmez ağ (2G, metro, asansör)
├── Pil kısıtlamaları (uyandırmaları minimize etme)
├── Sınırlı depolama (her şey önbelleğe alınamaz)
├── Kesitilen oturumlar (aramalar, bildirimler)
├── Çeşitli cihazlar (eski telefonlardan amiral gemilerine)
└── İkilik (binary) güncellemeler yavaştır (App Store incelemesi)
```

**Backend'iniz tüm bunları telafi etmelidir.**

---

## 🚫 YZ MOBİL BACKEND ANTİ-DESENLERİ

### Bunlar mobil backend inşa ederken YZ'lerin yaptığı yaygın hatalardır:

| ❌ YZ Varsayılanı | Neden Yanlış? | ✅ Mobil-Doğru |
|---------------|----------------|-------------------|
| Web ve mobil için aynı API | Mobilin kompakt yanıtlara ihtiyacı vardır | Ayrı mobil uç noktaları VEYA alan seçimi |
| Tam nesne yanıtları | Bant genişliği ve pil harcar | Kısmi yanıtlar, sayfalama |
| Çevrimdışı düşünülmemiş | Ağ olmadan uygulama çöker | Önce-çevrimdışı tasarım, senkronizasyon kuyrukları |
| Her şey için WebSocket | Pil tüketimi | Push bildirimleri + polling (yoklama) yedeği |
| Uygulama versiyonlaması yok | Güncelleme zorlanamaz, breaking change riski | Versiyon header'ları, minimum versiyon kontrolü |
| Genel hata mesajları | Kullanıcılar sorunu çözemez | Mobilde spesifik hata kodları + kurtarma eylemleri |
| Session tabanlı auth | Mobil uygulamalar sık kapanabilir | Refresh token destekli token tabanlı auth |
| Cihaz bilgisini yoksayma | Sorunlar hata ayıklanamaz | Header'larda Cihaz ID'si, uygulama versiyonu |

---

## 1. Push Bildirimleri (Push Notifications)

### Platform Mimarisi

```
┌─────────────────────────────────────────────────────────────────┐
│                    SİZİN BACKEND'İNİZ                            │
├─────────────────────────────────────────────────────────────────┤
│                         │                                        │
│              ┌──────────┴──────────┐                            │
│              ▼                     ▼                            │
│    ┌─────────────────┐   ┌─────────────────┐                    │
│    │   FCM (Google)  │   │  APNs (Apple)   │                    │
│    │   Firebase      │   │  Doğrudan/FCM   │                    │
│    └────────┬────────┘   └────────┬────────┘                    │
│             │                     │                              │
│             ▼                     ▼                              │
│    ┌─────────────────┐   ┌─────────────────┐                    │
│    │ Android Cihaz   │   │     iOS Cihaz   │                    │
│    └─────────────────┘   └─────────────────┘                    │
└─────────────────────────────────────────────────────────────────┘
```

### Push Türleri

| Tür | Kullanım Durumu | Kullanıcı Ne Görür? |
|------|----------|-----------|
| **Display (Görünür)** | Yeni mesaj, sipariş güncellemesi | Bildirim başlığı/banner |
| **Silent (Sessiz)** | Arka plan senk., içerik güncelleme | Hiçbir şey (arka planda) |
| **Data (Veri)** | Uygulama tarafından özel işleme | Uygulama mantığına bağlı |

### Anti-Desenler

| ❌ ASLA | ✅ HER ZAMAN |
|----------|----------|
| Push içinde hassas veri gönder | Push "Yeni mesaj" der, uygulama içeriği çeker |
| Push yağmuruna tut | Grupla, tekilleştir, sessiz saatlere saygı duy |
| Herkese aynı mesajı gönder | Kullanıcı tercihi ve zaman dilimine göre segmente et |
| Başarısız tokenları yoksay | Geçersiz tokenları düzenli olarak temizle |
| iOS için APNs'i atla | Sadece FCM ile iOS'ta teslimat garantisi yoktur |

---

## 2. Çevrimdışı Senk. ve Çakışma Çözümü

### Senkronizasyon Stratejisi Seçimi

```
VERİ TÜRÜ NEDİR?
        │
        ├── Salt Okunur (haberler, katalog)
        │   └── Basit önbellek + TTL
        │       └── Geçersiz kılma için ETag/Last-Modified
        │
        ├── Kullanıcıya Ait (notlar, yapılacaklar)
        │   └── Son yazan kazanır (basit)
        │       └── Veya zaman damgası tabanlı birleştirme
        │
        ├── İş Birlikli (paylaşılan dosyalar)
        │   └── CRDT veya OT gereklidir
        │       └── Firebase/Supabase değerlendirin
        │
        └── Kritik (ödemeler, envanter)
            └── Sunucu tek gerçeklik kaynağıdır
                └── İyimser UI + sunucu onayı
```

### Çakışma Çözümü (Conflict Resolution) Stratejileri

| Strateji | Nasıl Çalışır? | En İyi Kullanım |
|----------|--------------|----------|
| **Son yazan kazanır** | En yeni zaman damgası üzerine yazar | Basit veri, tek kullanıcı |
| **Sunucu kazanır** | Sunucu her zaman yetkilidir | Kritik işlemler |
| **İstemci kazanır** | Çevrimdışı değişiklikler önceliklidir | Çevrimdışı odaklı uygulamalar |
| **Birleştirme** | Alan bazında değişiklikleri birleştirir | Dokümanlar, zengin içerik |
| **CRDT** | Matematiksel olarak çakışmasız | Gerçek zamanlı iş birliği |

---

## 3. Mobil API Optimizasyonu

### Yanıt Boyutu Azaltma

| Teknik | Tasarruf | Uygulama |
|-----------|---------|----------------|
| **Alan seçimi** | 30-70% | `?fields=id,name,thumbnail` |
| **Sıkıştırma** | 60-80% | gzip/brotli (otomatik) |
| **Sayfalama** | Değişken | Mobil için cursor tabanlı |
| **Görsel varyasyonlar** | 50-90% | `/image?w=200&q=80` |
| **Delta senkronizasyonu**| 80-95% | Zaman damgasından sonraki değişiklikler |

---

## 4. Uygulama Versiyonlaması

### Versiyon Kontrol Uç Noktası (Endpoint)

```json
// GET /api/app-config
// Headers:
//   X-App-Version: 2.1.0
//   X-Platform: ios
//   X-Device-ID: abc123

{
  "minimum_version": "2.0.0",
  "latest_version": "2.3.0",
  "force_update": false,
  "update_url": "https://apps.apple.com/...",
  "feature_flags": {
    "new_player": true,
    "dark_mode": true
  },
  "maintenance": false,
  "maintenance_message": null
}
```

---

## 5. Mobil İçin Kimlik Doğrulama (Authentication)

### Token Stratejisi

```
ACCESS TOKEN:
├── Kısa ömürlü (15 dk - 1 saat)
├── Bellekte saklanır (kalıcı değil)
├── API istekleri için kullanılır
└── Süresi dolduğunda yenilenir

REFRESH TOKEN:
├── Uzun ömürlü (30-90 gün)
├── SecureStore/Keychain içinde saklanır
├── Sadece yeni access token almak için kullanılır
└── Her kullanımda yenilenir (güvenlik için rotate)

DEVICE TOKEN:
├── Bu cihazı tanımlar
├── "Tüm cihazlardan çıkış yap" imkanı sunar
├── Refresh token ile birlikte saklanır
└── Sunucu aktif cihazları takip eder
```

---

## 6. Mobil İçin Hata Yönetimi

### Mobil-Özel Hata Formatı

```json
{
  "error": {
    "code": "PAYMENT_DECLINED",
    "message": "Ödemeniz reddedildi",
    "user_message": "Lütfen kart bilgilerinizi kontrol edin veya başka bir yöntem deneyin",
    "action": {
      "type": "navigate",
      "destination": "payment_methods"
    },
    "retry": {
      "allowed": true,
      "after_seconds": 5
    }
  }
}
```

---

## 7. Medya ve Binary İşleme

### Görsel Optimizasyonu

```
İSTEMCİ İSTEĞİ:
GET /images/{id}?w=400&h=300&q=80&format=webp

SUNUCU YANITI:
├── Anlık boyutlandırma VEYA CDN kullanımı
├── Android için WebP (daha küçük)
├── iOS 14+ için HEIC (destekleniyorsa)
├── JPEG yedeği
└── Cache-Control: max-age=31536000
```

---

## 8. Mobil Güvenlik

### Cihaz Doğrulaması (Attestation)

```
GERÇEK CİHAZ DOĞRULAMA (emülatör/bot değil):
├── iOS: DeviceCheck API (Sunucu Apple ile doğrular)
├── Android: Play Integrity API (Sunucu Google ile doğrular)
└── Fail closed: Doğrulama başarısızsa reddet
```

### İstek İmzalama (Request Signing)

```
İSTEMCİ:
├── İmza oluşturur = HMAC(zaman damgası + yol + gövde, secret)
├── Gönderir: X-Signature: {imza}
├── Gönderir: X-Timestamp: {zaman_damgası}
└── Gönderir: X-Device-ID: {cihaz_id}

SUNUCU:
├── Zaman damgasını doğrular (5 dakika içinde)
├── Aynı girdilerle imzayı tekrar oluşturur
├── İmzaları karşılaştırır
└── Eşleşmezse reddeder (veri kurcalanmış demektir)
```

---

## 📝 MOBİL BACKEND KONTROL LİSTESİ

- [ ] **Mobil-özel gereksinimler belirlendi mi?**
- [ ] **Çevrimdışı davranış planlandı mı?**
- [ ] **Yanıtlar olabildiğince küçük mü?**
- [ ] **Token yenileme (refresh) uygulandı mı?**
- [ ] **Hassas veri push mesajı içinde gönderiliyor mu? (GÖNDERİLMEMELİ)**
- [ ] **Versiyon kontrol ucu (endpoint) hazır mı?**
- [ ] **Cihaz ID'si, uygulama versiyonu vb. header'lar ekleniyor mu?**

---

> **Unutma:** Mobil backend kötü ağlara dayanıklı olmalı, pil ömrüne saygı duymalı ve kesilen oturumları zarafetle yönetmelidir. İstemciye (client) güvenilemez ama onu tıkanmış halde de bırakamazsınız; çevrimdışı yetenekler ve net hata kurtarma yolları sağlayın.
