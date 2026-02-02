---
name: game-art
description: Oyun sanatı (Game art) prensipleri. Görsel stil seçimi, varlık boru hattı, animasyon iş akışı.
allowed-tools: Read, Glob, Grep
---

# Oyun Sanatı (Game Art) Prensipleri

> Oyunlar için görsel tasarım düşüncesi - stil seçimi, varlık (asset) boru hattı ve sanat yönetimi.

---

## 1. Sanat Stili Seçimi

### Karar Ağacı

```
Oyun hangi duyguyu uyandırmalı?
│
├── Nostaljik / Retro
│   ├── Sınırlı palet mi? → Pixel Art
│   └── El çizimi hissi mi? → Vektör / Flash stili
│
├── Gerçekçi / Derinlikli (Immersive)
│   ├── Yüksek bütçe mi? → PBR 3B (PBR 3D)
│   └── Stilize gerçekçilik mi? → El boyaması (Hand-painted) dokular
│
├── Cana Yakın / Şirin (Casual)
│   ├── Net şekiller mi? → Flat / Minimalist
│   └── Yumuşak bir his mi? → Gradyan / Yumuşak gölgeler
│
└── Benzersiz / Deneysel
    └── Özel bir stil rehberi tanımlayın
```

### Stil Karşılaştırma Matrisi

| Stil | Üretim Hızı | Yetenek Eşiği | Ölçeklenebilirlik | En Uygun |
|-------|------------------|-------------|-------------|----------|
| **Pixel Art** | Orta | Orta | Ekip bulmak zor | Bağımsız, retro |
| **Vektör/Flat** | Hızlı | Düşük | Kolay | Mobil, şirin oyunlar |
| **El Boyaması** | Yavaş | Yüksek | Orta | Fantezi, stilize |
| **PBR 3B** | Yavaş | Yüksek | AAA boru hattı | Gerçekçi oyunlar |
| **Low-poly** | Hızlı | Orta | Kolay | Bağımsız 3B |
| **Cel-shaded** | Orta | Orta | Orta | Anime, çizgi film |

---

## 2. Varlık (Asset) Boru Hattı Kararları

### 2B Boru Hattı

| Aşama | Araç Seçenekleri | Çıktı |
|-------|--------------|--------|
| **Konsept** | Kağıt, Procreate, Photoshop | Referans sayfası |
| **Yaratım** | Aseprite, Photoshop, Krita | Tekil sprite'lar |
| **Atlas** | TexturePacker, Aseprite | Spritesheet |
| **Animasyon** | Spine, DragonBones, Kare-kare | Animasyon verisi |
| **Entegrasyon** | Oyun Motoru | Oyuna hazır varlıklar |

### 3B Boru Hattı

| Aşama | Araç Seçenekleri | Çıktı |
|-------|--------------|--------|
| **Konsept** | 2B sanat, Blockout | Referans |
| **Modelleme** | Blender, Maya, 3ds Max | Yüksek poligonlu mesh |
| **Retopoloji** | Blender, ZBrush | Oyuna hazır mesh |
| **UV/Dokulama** | Substance Painter, Blender | Doku haritaları (Texture maps) |
| **Rigleme** | Blender, Maya | İskelet sistemi (Rig) |
| **Animasyon** | Blender, Maya, Mixamo | Animasyon klipleri |
| **Dışa Aktarma** | FBX, glTF | Motor için hazır dosya |

---

## 3. Renk Teorisi Kararları

### Palet Seçimi

| Hedef | Strateji | Örnek |
|------|----------|---------|
| **Uyum** | Tamamlayıcı veya benzer renkler | Doğa oyunları |
| **Kontrast** | Yüksek doygunluk farkları | Aksiyon oyunları |
| **Ruh Hali** | Sıcak/soğuk sıcaklığı | Korku, huzurlu oyunlar |
| **Okunabilirlik** | Renk tonu yerine değer kontrastı | Oynanış netliği |

### Renk Prensipleri

- **Hiyerarşi:** Önemli öğeler öne çıkmalıdır.
- **Tutarlılık:** Aynı nesne = aynı renk ailesi.
- **Bağlam:** Renkler farklı arka planlarda farklı okunur.
- **Erişilebilirlik:** Sadece renge güvenmeyin (şekil farkı ekleyin).

---

## 4. Animasyon Prensipleri

### 12 Prensip (Oyunlara Uygulanmış Hali)

| Prensip | Oyun Uygulaması |
|-----------|------------------|
| **Esnetme ve Ezme** | Zıplama kavisleri, etkiler |
| **Beklenti (Anticipation)** | Saldırıdan önce yapılan hazırlık |
| **Sahneleme (Staging)** | Net silüetler |
| **Takip ve Üst Üste Binme** | Hareketten sonra saç/pelerin savrulması |
| **Giriş ve Çıkışta Yavaşlama** | Geçişlerde yumuşatma (easing) |
| **Kavisler (Arcs)** | Doğal hareket yolları |
| **İkincil Eylem** | Nefes alma, göz kırpma |
| **Zamanlama** | Kare sayısı = ağırlık/hız |
| **Mübalağa (Exaggeration)** | Uzaktan okunabilir olması |
| **Cazibe (Appeal)** | Akılda kalıcı tasarım |

### Kare Sayısı Yönergeleri

| Eylem Türü | Tipik Kare Sayısı | Hissi |
|-------------|----------------|------|
| Nefes alma | 4-8 | Hafif |
| Yürüme döngüsü | 6-12 | Yumuşak |
| Koşma döngüsü | 4-8 | Enerjik |
| Saldırı | 3-6 | Hızlı/Sert |
| Ölüm | 8-16 | Dramatik |

---

## 5. Çözünürlük ve Ölçek Kararları

### Platforma Göre 2B Çözünürlük

| Platform | Temel Çözünürlük | Sprite Ölçeği |
|----------|-----------------|--------------|
| Mobil | 1080p | 64-128px karakterler |
| Masaüstü | 1080p-4K | 128-256px karakterler |
| Pixel art | 320x180 - 640x360 | 16-32px karakterler |

### Tutarlılık Kuralı

Bir temel birim seçin ve ona sadık kalın:
- Pixel art: 1x boyutunda çalışın, yukarı ölçeklendirin (asla aşağı değil).
- HD sanat: Bir DPI tanımlayın, oranı koruyun.
- 3B: 1 birim = 1 metre (endüstri standardı).

---

## 6. Varlık (Asset) Organizasyonu

### İsimlendirme Kuralları

```
[tür]_[nesne]_[varyant]_[durum].[uzanti]

Örnekler:
spr_oyuncu_bekleme_01.png
tex_tas_duvar_normal.png
mesh_agac_mese_lod2.fbx
```

### Klasör Yapısı Prensibi

```
varliklar/ (assets/)
├── karakterler/
│   ├── oyuncu/
│   └── dusmanlar/
├── cevre/
│   ├── dekorlar/
│   └── karolar (tiles)/
├── arayüz (ui)/
├── efektler/
└── ses (audio)/
```

---

## 7. Anti-Desenler (Yapılmaması Gerekenler)

| YAPMAYIN | YAPIN |
|-------|-----|
| Sanat stillerini rastgele karıştırmak | Stil rehberi tanımlayın ve ona uyun |
| Sadece final çözünürlükte çalışmak | Kaynak çözünürlükte yaratın |
| Silüet okunabilirliğini görmezden gelmek | Oynanış mesafesinden test edin |
| Arkaplanı aşırı detaylandırmak | Detayı oyuncu bölgesine odaklayın |
| Renk testini atlamak | Hedef ekranda test edin |

---

> **Unutmayın:** Sanat oyun mekaniğine hizmet eder. Eğer oyuncuya yardımcı olmuyorsa, o sadece bir süstür.
