---
name: multiplayer
description: Çok oyunculu (Multiplayer) oyun geliştirme prensipleri. Mimari, ağ iletişimi, senkronizasyon.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash
---

# Çok Oyunculu Oyun Geliştirme (Multiplayer Game Development)

> Ağ mimarisi ve senkronizasyon prensipleri.

---

## 1. Mimari Seçimi

### Karar Ağacı

```
Ne tür bir çok oyunculu deneyim?
│
├── Rekabetçi / Gerçek Zamanlı
│   └── Dedicated Server (Yetkili Sunucu)
│
├── İşbirlikçi (Co-op) / Gündelik (Casual)
│   └── Host-tabanlı (Bir oyuncu sunucu olur)
│
├── Sıra Tabanlı
│   └── Client-server (Basit yapı)
│
└── Devasa (MMO)
    └── Dağıtık sunucular (Distributed)
```

### Karşılaştırma

| Mimari | Gecikme (Latency) | Maliyet | Güvenlik |
|--------------|---------|------|----------|
| **Dedicated** | Düşük | Yüksek | Güçlü |
| **P2P** | Değişken | Düşük | Zayıf |
| **Host-tabanlı** | Orta | Düşük | Orta |

---

## 2. Senkronizasyon Prensipleri

### Durum (State) vs Girdi (Input)

| Yaklaşım | Ne Senkronize Edilir? | En Uygun |
|----------|-----------|----------|
| **Durum Senkronizasyonu** | Oyun durumu | Basit, az nesneli oyunlar |
| **Girdi Senkronizasyonu** | Oyuncu girdileri | Aksiyon oyunları |
| **Hibrit** | Her ikisi | Çoğu modern oyun |

### Gecikme Telafisi (Lag Compensation)

| Teknik | Amaç |
|-----------|---------|
| **Tahmin (Prediction)** | İstemci sunucuyu tahmin eder |
| **Interpolasyon** | Uzaktaki oyuncuları akıcı gösterir |
| **Uzlaşma (Reconciliation)** | Hatalı tahminleri düzeltir |
| **Gecikme Telafisi** | Vuruş tespiti için zamanı geri sarar |

---

## 3. Ağ Optimizasyonu

### Bant Genişliğini Azaltma

| Teknik | Kazanç |
|-----------|---------|
| **Delta sıkıştırma** | Sadece değişiklikleri gönder |
| **Kuantizasyon** | Hassasiyeti (precision) azalt |
| **Önceliklendirme** | Önce önemli verileri gönder |
| **İlgi Alanı (AOI)** | Sadece yakındaki varlıkları gönder |

### Güncelleme Hızları (Update Rates)

| Tür | Hız |
|------|------|
| Konum | 20-60 Hz |
| Sağlık | Değiştiğinde |
| Envanter | Değiştiğinde |
| Sohbet | Gönderildiğinde |

---

## 4. Güvenlik Prensipleri

### Sunucu Otoritesi (Server Authority)

```
İstemci: "Düşmana vurdum"
Sunucu: Doğrula → Mermi gerçekten değdi mi?
         → Oyuncu geçerli bir durumda mıydı?
         → Bu zamanlamayla bu hareket mümkün mü?
```

### Anti-Hile (Anti-Cheat)

| Hile Türü | Önleme Yöntemi |
|-------|------------|
| Hız hilesi (Speed hack) | Sunucu hareketi doğrular |
| Aimbot | Sunucu görüş hattını doğrular |
| Eşya kopyalama | Envanter sunucu kontrolündedir |
| Duvar hilesi (Wall hack) | Görünmeyen veriyi gönderilmez |

---

## 5. Eşleştirme (Matchmaking)

### Hususlar

| Faktör | Etki |
|--------|--------|
| **Yetenek (Skill)** | Adil maçlar |
| **Gecikme (Latency)** | Oynanabilir bağlantı |
| **Bekleme Süresi** | Oyuncu sabrı |
| **Grup Boyutu** | Ekip halinde oynama |

---

## 6. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| İstemciye güvenmek | Otorite her zaman sunucudur |
| Her şeyi göndermek | Sadece gerekli olanı gönderin |
| Gecikmeyi yok saymak | 100-200ms gecikmeyi hesaba katın |
| Tam konumları eşitlemek | Tahmin/Interpolasyon kullanın |

---

> **Unutmayın:** İstemciye (client) asla güvenmeyin. Gerçeğin tek kaynağı sunucudur.
