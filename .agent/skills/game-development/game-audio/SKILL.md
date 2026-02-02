---
name: game-audio
description: Oyun ses (game audio) prensipleri. Ses tasarımı, müzik entegrasyonu, adaptif ses sistemleri.
allowed-tools: Read, Glob, Grep
---

# Oyun Ses (Game Audio) Prensipleri

> Derinlikli oyun deneyimleri için ses tasarımı ve müzik entegrasyonu.

---

## 1. Ses Kategori Sistemi

### Kategori Tanımları

| Kategori | Davranış | Örnekler |
|----------|----------|----------|
| **Müzik** | Döngüye girer, crossfade, ducking | BGM, savaş müziği |
| **SFX** | Tek seferlik (One-shot), 3B konumlandırılmış | Ayak sesleri, darbeler |
| **Ambiyans** | Döngüye girer, arka plan katmanı | Rüzgar, kalabalık, orman |
| **UI (Arayüz)** | Anlık, 3B olmayan | Buton tıklamaları, bildirimler |
| **Voice (Ses)** | Öncelik, ducking tetikleyici | Diyaloglar, sunucu |

### Öncelik Hiyerarşisi

```
Sesler kanallar için yarıştığında:

1. Voice (Ses - En yüksek, her zaman duyulabilir)
2. Player SFX (Oyuncu - Geri bildirim kritiktir)
3. Enemy SFX (Düşman - Oynanış için gereklidir)
4. Music (Müzik - Ruh hali verir ama sönümlenebilir)
5. Ambient (Ambiyans - En düşük, kanal dolduğunda kesilebilir)
```

---

## 2. Ses Tasarımı Kararları

### SFX Oluşturma Yaklaşımı

| Yaklaşım | Ne Zaman Kullanılır | Artıları/Eksileri |
|----------|-------------|------------|
| **Kayıt (Recording)** | Gerçekçi ihtiyaçlar | Yüksek kalite, zaman alır |
| **Sentez (Synthesis)** | Bilim kurgu, retro, UI | Benzersiz, yetenek gerektirir |
| **Kütüphane Örnekleri**| Hızlı üretim | Yaygın sesler, lisanslama |
| **Katmanlama (Layering)**| Karmaşık sesler | En iyi sonuçlar, çok emek |

### Katmanlama Yapısı

| Katman | Amaç | Örnek: Silah Sesi |
|-------|---------|------------------|
| **Attack (Atak)** | İlk geçiş anı (transient) | Tık, çıt sesi |
| **Body (Gövde)** | Ana karakter | Güm, patlama |
| **Tail (Kuyruk)** | Sönümlenme, oda tınısı | Reverb, eko |
| **Sweetener** | "Gizli sos" | Boş kovan sesi, mekanik sesler |

---

## 3. Müzik Entegrasyonu

### Müzik Durum Sistemi

```
Oyun Durumu → Müzik Tepkisi
│
├── Menü → Sakin, döngüsel tema
├── Keşif → Ambiyans odaklı, atmosferik
├── Tehlike Algılandı → Gerilime geçiş
├── Çatışma Başladı → Tam savaş müziği
├── Galibiyet → Kısa final sesi (stinger) + sakin geçiş
├── Mağlubiyet → Hazin final sesi
└── Boss → Benzersiz, çok aşamalı parça
```

### Geçiş Teknikleri

| Teknik | Ne Zaman Kullanılır | Hissi |
|-----------|----------|------|
| **Crossfade** | Yumuşak ruh hali değişimi | Kademeli |
| **Stinger** | Anlık olay | Dramatik |
| **Stem mixing** | Dinamik yoğunluk | Kesintisiz |
| **Beat-synced** | Ritmik oynanış | Müzikal |
| **Queue point** | Bir sonraki doğal ara | Temiz |

---

## 4. Adaptif Ses Kararları

### Yoğunluk Parametreleri

| Parametre | Neyi Etkiler | Örnek |
|-----------|---------|---------|
| **Tehdit Seviyesi** | Müzik yoğunluğu | Düşman sayısı |
| **Sağlık** | Filtre, reverb | Düşük sağlık = boğuk ses |
| **Hız** | Tempo, enerji | Yarış hızı |
| **Çevre** | Reverb, EQ | Mağara vs açık alan |
| **Günün Saati** | Ruh hali, ses seviyesi | Gece = daha sessiz |

### Dikey (Vertical) vs Yatay (Horizontal)

| Sistem | Ne Değişir | En Uygun |
|--------|--------------|----------|
| **Dikey (katmanlar)** | Enstrüman katmanları ekle/çıkar | Yoğunluk ölçeklendirme |
| **Yatay (segmentler)** | Farklı müzik bölümleri | Durum değişiklikleri |
| **Birleşik** | Her ikisi | AAA adaptif müzikler |

---

## 5. 3B Ses (3D Audio) Kararları

### Uzamsallaştırma (Spatialization)

| Öğe | 3B Konumlandırılmış mı? | Neden? |
|---------|----------------|--------|
| Oyuncu ayak sesleri | Hayır (veya çok hafif) | Her zaman duyulur |
| Düşman ayak sesleri | Evet | Yönsel farkındalık |
| Silah sesleri | Evet | Çatışma farkındalık |
| Müzik | Hayır | Ruh hali, sahne dışı (non-diegetic) |
| Ambiyans alanı | Evet (alan bazlı) | Çevresel etki |
| UI sesleri | Hayır | Arayüz geri bildirimi |

### Mesafe Davranışı

| Mesafe | Ses Davranışı |
|----------|----------------|
| **Yakın** | Tam ses seviyesi, tam frekans |
| **Orta** | Ses seviyesi azalır, yüksek frekanslar düşer |
| **Uzak** | Düşük ses, low-pass filtre (bas odaklı) |
| **Maksimum** | Sessiz veya çok hafif bir ipucu |

---

## 6. Platform Hususları

### Format Seçimi

| Platform | Önerilen Format | Neden? |
|----------|-------------------|--------|
| PC | OGG Vorbis, WAV | Kalite, lisanssız |
| Konsol | Platforma özel | Sertifikasyon |
| Mobil | MP3, AAC | Boyut, uyumluluk |
| Web | WebM/Opus, MP3 yedek | Tarayıcı desteği |

### Bellek Bütçesi

| Oyun Türü | Ses Bütçesi | Strateji |
|-----------|--------------|----------|
| Mobil (Casual) | 10-50 MB | Sıkıştırılmış, az varyasyon |
| Bağımsız PC | 100-500 MB | Kalite odaklı |
| AAA | 1+ GB | Tam kalite, çok sayıda varyasyon |

---

## 7. Miks Hiyerarşisi

### Ses Seviyesi Dengesi Referansı

| Kategori | Göreceli Seviye | Notlar |
|----------|----------------|-------|
| **Voice (Ses)** | 0 dB (referans) | Her zaman net |
| **Player SFX** | -3 ile -6 dB arası | Belirgin ama sert değil |
| **Music (Müzik)** | -6 ile -12 dB arası | Temel, ses girdiğinde sönümlenir |
| **Enemy SFX** | -6 ile -9 dB arası | Önemli ama baskın değil |
| **Ambiyans** | -12 ile -18 dB arası | Hafif arka plan |

### Sönümleme (Ducking) Kuralları

| Ne Zaman | Neyi Sönümle | Miktar |
|------|-----------|--------|
| Ses (diyalog) çaldığında | Müzik, Ambiyans | -6 ile -9 dB arası |
| Patlama olduğunda | Patlama dışındaki her şeyi | Kısa süreli sönümleme |
| Menü açıldığında | Oynanış seslerini | -3 ile -6 dB arası |

---

## 8. Anti-Desenler (Yapılmaması Gerekenler)

| YAPMAYIN | YAPIN |
|-------|-----|
| Aynı sesi defalarca çalmak | Varyasyon kullanın (ses başına 3-5 adet) |
| Her şeyin sesini maksimize etmek| Doğru miks hiyerarşisi kullanın |
| Sessizliği görmezden gelmek | Sessizlik kontrast yaratır |
| Tek bir müzik parçasını sonsuza dek döndürmek | Çeşitlilik ve geçişler sunun |
| Prototipte sesi es geçmek | Yer tutucu (placeholder) sesler bile önemlidir |

---

> **Unutmayın:** Oyun deneyiminin %50'si sestir. Sessiz bir oyun ruhunun yarısını kaybeder.
