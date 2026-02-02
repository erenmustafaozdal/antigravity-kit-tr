---
name: game-design
description: Oyun tasarımı (Game design) prensipleri. GDD yapısı, dengeleme, oyuncu psikolojisi, ilerleme.
allowed-tools: Read, Glob, Grep
---

# Oyun Tasarımı (Game Design) Prensipleri

> Sürükleyici oyunlar için tasarım düşüncesi.

---

## 1. Temel Döngü (Core Loop) Tasarımı

### 30 Saniye Testi

```
Her oyunun eğlenceli bir 30 saniyelik döngüye ihtiyacı vardır:
1. EYLEM (ACTION) → Oyuncu bir şey yapar
2. GERİ BİLDİRİM (FEEDBACK) → Oyun tepki verir
3. ÖDÜL (REWARD) → Oyuncu iyi hisseder
4. TEKRAR (REPEAT)
```

### Döngü Örnekleri

| Tür | Temel Döngü |
|-------|-----------|
| Platformer | Koş → Zıpla → Kon → Topla |
| Shooter | Nişan Al → Ateş Et → Öldür → Yağmala |
| Bulmaca | Gözlemle → Düşün → Çöz → İlerle |
| RPG | Keşfet → Savaş → Seviye Atla → Ekipman Diz |

---

## 2. Oyun Tasarım Belgesi (Game Design Document - GDD)

### Temel Bölümler

| Bölüm | İçerik |
|---------|---------|
| **Pitch (Tanıtım)**| Tek cümlelik açık açıklama |
| **Temel Döngü** | 30 saniyelik oynanış özeti |
| **Mekanikler** | Sistemlerin nasıl çalıştığı |
| **İlerleme** | Oyuncunun nasıl yol katettiği |
| **Sanat Stili** | Görsel yönelim |
| **Ses (Audio)** | Ses ve müzik yönelimi |

### Prensipler

- Belgeyi canlı tutun (düzenli olarak güncelleyin).
- Görseller iletişimi kolaylaştırır.
- Az ama öz (küçük başlayın).

---

## 3. Oyuncu Psikolojisi

### Motivasyon Türleri

| Tür | İtici Güç |
|------|-----------|
| **Başarı Odaklı (Achiever)**| Hedefler, tamamlama |
| **Kâşif (Explorer)**| Keşif, sırlar |
| **Sosyal (Socializer)**| Etkileşim, topluluk |
| **Rekabetçi (Killer)**| Rekabet, baskınlık |

### Ödül Takvimleri

| Takvim | Etki | Kullanım |
|----------|--------|-----|
| **Sabit (Fixed)** | Tahmin edilebilir | Kilometre taşı ödülleri |
| **Değişken (Variable)**| Bağımlılık yapıcı | Yağma (loot) dropları |
| **Oran (Ratio)** | Çaba tabanlı | Grind odaklı oyunlar |

---

## 4. Zorluk Dengeleme

### Akış Durumu (Flow State)

```
Çok Zor → Hayal Kırıklığı → Oyunu Bırakma
Çok Kolay → Sıkılma → Oyunu Bırakma
Tam Ayarında → Akış (Flow) → Bağlılık
```

### Dengeleme Stratejileri

| Strateji | Nasıl Uygulanır |
|----------|-----|
| **Dinamik** | Oyuncunun yeteneğine göre ayarla |
| **Seçim** | Zorluğu oyuncunun seçmesine izin ver |
| **Erişilebilirlik** | Herkes için seçenekler sun |

---

## 5. İlerleme Tasarımı (Progression)

### İlerleme Türleri

| Tür | Örnek |
|------|---------|
| **Yetenek (Skill)**| Oyuncu bizzat ustalaşır |
| **Güç (Power)** | Karakterin istatistikleri güçlenir |
| **İçerik** | Yeni bölgelerin kilidi açılır |
| **Hikaye** | Anlatı ilerler |

### Tempo Prensipleri

- Erken kazanımlar (kullanıcıyı hemen yakalayın).
- Zorluğu kademeli olarak artırın.
- Yoğunluk arasuna dinlenme anları (rest beats) koyun.
- Anlamlı seçimler sunun.

---

## 6. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Tek başınıza tasarım yapmak | Sürekli oyun testi (playtest) yapın |
| Eğlenceyi bulmadan cilalamak | Önce prototip üretin |
| Tek bir oynanış tarzını zorlamak | Oyuncunun kendini ifade etmesine izin verin |
| Aşırı cezalandırmak | İlerlemeyi ödüllendirin |

---

> **Unutmayın:** Eğlence kağıt üzerinde tasarlanmaz, deneme-yanılma (iteration) yoluyla keşfedilir.
