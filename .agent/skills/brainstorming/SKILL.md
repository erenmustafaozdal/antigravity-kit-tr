---
name: brainstorming
description: Sokratik sorgulama protokolü + kullanıcı iletişimi. Karmaşık istekler, yeni özellikler veya belirsiz gereksinimler için ZORUNLUDUR. İlerleme raporlamasını ve hata yönetimini içerir.
allowed-tools: Read, Glob, Grep
---

# Beyin Fırtınası ve İletişim Protokolü

> **ZORUNLU:** Karmaşık/belirsiz istekler, yeni özellikler ve güncellemeler için kullanın.

---

## 🛑 SOKRATİK GEÇİT (UYGULAMA)

### Ne Zaman Tetiklenir?

| Durum | Eylem |
|---------|--------|
| Detay verilmeden "[Şeyi] yap/oluştur" dendiğinde | 🛑 3 soru SORUN |
| Karmaşık özellik veya mimari taleplerinde | 🛑 Uygulamadan önce netleştirin |
| Güncelleme/değişiklik isteklerinde | 🛑 Kapsamı doğrulayın |
| Belirsiz gereksinimlerde | 🛑 Amacı, kullanıcıları ve kısıtlamaları sorun |

### 🚫 ZORUNLU: Uygulama Öncesi 3 Soru

1. **DUR** - Hemen kod yazmaya başlamayın.
2. **SOR** - En az 3 temel soru sorun:
   - 🎯 Amaç: Hangi sorunu çözüyorsunuz?
   - 👥 Kullanıcılar: Bunu kimler kullanacak?
   - 📦 Kapsam: Olmazsa olmazlar vs. olsa iyi olur dedikleriniz neler?
3. **BEKLE** - Devam etmeden önce kullanıcının yanıtını alın.

---

## 🧠 Dinamik Soru Üretimi

**⛔ ASLA statik şablonlar kullanmayın.** Prensipler için `dynamic-questioning.md` dosyasını okuyun.

### Temel Prensipler

| Prensip | Anlamı |
|-----------|---------|
| **Sorular Sonuçları Belirler** | Her soru bir mimari karara bağlanmalıdır |
| **İçerikten Önce Bağlam** | Önce bağlamı (yeni proje/özellik/refactor/debug) anlayın |
| **Minimum Gerekli Sorular** | Her soru bir uygulama yolunu elemelidir |
| **Varsayım Değil, Veri Üret** | Tahmin etmeyin; takasları (trade-offs) sunarak sorun |

### Soru Üretme Süreci

```
1. İsteği Çözümle → Alanı, özellikleri ve ölçek göstergelerini çıkar
2. Karar Noktalarını Belirle → Engelleyici (blocking) vs. ertelenebilir kararlar
3. Soruları Üret → Öncelik: P0 (engelleyici) > P1 (yüksek kaldıraçlı) > P2 (olsa iyi olur)
4. Takaslarla Formatla → Ne, Neden, Seçenekler, Varsayılan değer
```

### Soru Formatı (ZORUNLU)

```markdown
### [ÖNCELİK] **[KARAR NOKTASI]**

**Soru:** [Net soru cümlesi]

**Bu Neden Önemli:**
- [Mimari sonuç/etki]
- [Etkilenen alanlar: maliyet/karmaşıklık/zaman çizelgesi/ölçek]

**Seçenekler:**
| Seçenek | Artılar | Eksiler | En Uygun Durum |
|--------|------|------|----------|
| A | [+] | [-] | [Senaryo] |

**Belirtilmezse:** [Varsayılan değer + gerekçesi]
```

**Detaylı alan bazlı soru bankaları ve algoritmalar için bakınız:** `dynamic-questioning.md`

---

## İlerleme Raporlaması (PRENSİP TABANLI)

**PRENSİP:** Şeffaflık güven oluşturur. Durum görünür ve aksiyon alınabilir olmalıdır.

### Durum Panosu Formatı

| Ajan | Durum | Mevcut Görev | İlerleme |
|-------|--------|--------------|----------|
| [Ajan Adı] | ✅🔄⏳❌⚠️ | [Görev açıklaması] | [% veya sayı] |

### Durum İkonları

| İkon | Anlamı | Kullanım |
|------|---------|-------|
| ✅ | Tamamlandı | Görev başarıyla bitti |
| 🔄 | Çalışıyor | Şu an yürütülüyor |
| ⏳ | Bekliyor | Engellendi, bağımlılık bekleniyor |
| ❌ | Hata | Başarısız oldu, müdahale gerekiyor |
| ⚠️ | Uyarı | Potansiyel sorun, engelleyici değil |

---

## Hata Yönetimi (PRENSİP TABANLI)

**PRENSİP:** Hatalar net iletişim için birer fırsattır.

### Hata Yanıt Deseni

```
1. Hatayı kabul et
2. Neler olduğunu açıkla (kullanıcı dostu dilde)
3. Takaslarla birlikte spesifik çözümler sun
4. Kullanıcıdan birini seçmesini veya alternatif belirtmesini iste
```

### Hata Kategorileri

| Kategori | Yanıt Stratejisi |
|----------|-------------------|
| **Port Çakışması** | Alternatif port öner veya mevcut olanı kapatmayı teklif et |
| **Eksik Bağımlılık** | Otomatik kur veya izin iste |
| **Build Hatası** | Spesifik hatayı + önerilen düzeltmeyi göster |
| **Belirsiz Hata** | Detay iste: ekran görüntüsü, konsol çıktısı vb. |

---

## Tamamlama Mesajı (PRENSİP TABANLI)

**PRENSİP:** Başarıyı kutlayın, sonraki adımlara rehberlik edin.

### Tamamlama Yapısı

```
1. Başarı onayı (kısa bir kutlama)
2. Yapılanların özeti (somut maddeler)
3. Nasıl doğrulanır/test edilir (aksiyon alınabilir)
4. Sonraki adım önerisi (proaktif)
```

---

## İletişim Prensipleri

| Prensip | Uygulama |
|-----------|----------------|
| **Öz** | Gereksiz detay yok, hedefe odaklan |
| **Görsel** | Hızlı tarama için emojileri (✅🔄⏳❌) kullan |
| **Spesifik** | "Biraz bekle" yerine "~2 dakika" |
| **Alternatifli** | Takılındığında birden fazla yol sun |
| **Proaktif** | Tamamlandıktan sonraki adımı öner |

---

## Anti-Desenler (KAÇININ)

| Anti-Desen | Neden? |
|--------------|-----|
| Anlamadan çözüme atlamak | Yanlış sorun üzerinde zaman kaybettirir |
| Sormadan gereksinim varsaymak | Yanlış çıktı üretir |
| İlk versiyonda aşırı mühendislik | Değer teslimini geciktirir |
| Kısıtlamaları görmezden gelmek | Kullanılamaz çözümler yaratır |
| "Bence" gibi ifadeler | Belirsizlik yaratır → Bunun yerine sorun |
