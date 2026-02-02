---
name: geo-fundamentals
description: AI arama motorları (ChatGPT, Claude, Perplexity vb.) için Üretken Motor Optimizasyonu (GEO).
allowed-tools: Read, Glob, Grep
---

# GEO Temelleri (Generative Engine Optimization)

> Yapay zeka destekli arama motorları için optimizasyon.

---

## 1. GEO Nedir?

**GEO** = Generative Engine Optimization (Üretken Motor Optimizasyonu)

| Hedef | Platformlar |
|------|----------|
| YZ yanıtlarında kaynak gösterilmek | ChatGPT, Claude, Perplexity, Gemini |

### SEO vs GEO

| Özellik | SEO | GEO |
|--------|-----|-----|
| Hedef | 1. sırada yer almak | YZ alıntıları/kaynakları |
| Platform | Google, Bing | YZ motorları |
| Metrikler | Sıralama, Tıklama Oranı (CTR) | Alıntılanma oranı |
| Odak | Anahtar kelimeler | Varlıklar (Entities), veriler |

---

## 2. YZ Motor Eko-Sistemi

| Motor | Alıntı Tarzı | Fırsat |
|--------|----------------|-------------|
| **Perplexity** | Numaralandırılmış [1][2] | En yüksek alıntılanma oranı |
| **ChatGPT** | Satır içi / alt bilgi | Özel GPT'ler |
| **Claude** | Bağlamsal | Uzun içerikli materyaller |
| **Gemini** | Kaynaklar bölümü | SEO ile ortak noktalar |

---

## 3. RAG Erişim Faktörleri

YZ motorlarının alıntı yapacak içeriği nasıl seçtiği:

| Faktör | Ağırlık |
|--------|--------|
| Anlamsal alaka (Semantic relevance) | ~%40 |
| Anahtar kelime eşleşmesi | ~%20 |
| Otorite sinyalleri | ~%15 |
| Güncellik | ~%10 |
| Kaynak çeşitliliği | ~%15 |

---

## 4. Alıntılanan İçerik Türleri

| Öğe | Neden İşe Yarar? |
|---------|--------------|
| **Özgün istatistikler** | Benzersiz, alıntılanabilir veri |
| **Uzman görüşleri** | Otorite aktarımı |
| **Net tanımlar** | Ayıklanması kolaydır |
| **Adım adım kılavuzlar** | Uygulanabilir değer sunar |
| **Karşılaştırma tabloları** | Yapılandırılmış bilgi |
| **SSS (FAQ) bölümleri** | Doğrudan cevaplar |

---

## 5. GEO İçerik Kontrol Listesi

### İçerik Öğeleri

- [ ] Soru tabanlı başlıklar
- [ ] En üstte özet / TL;DR
- [ ] Kaynakları belirtilmiş özgün veriler
- [ ] Uzman görüşleri (isim, ünvan ile)
- [ ] SSS bölümü (3-5 soru-cevap)
- [ ] Net tanımlar
- [ ] "Son güncelleme" zaman damgası
- [ ] Kimlik bilgileriyle birlikte yazar bilgisi

### Teknik Öğeler

- [ ] Tarih içeren Article şeması (Schema.org)
- [ ] Yazar için Person şeması
- [ ] FAQPage şeması
- [ ] Hızlı yükleme (< 2.5 sn)
- [ ] Temiz HTML yapısı

---

## 6. Varlık İnşası (Entity Building)

| Eylem | Amaç |
|--------|---------|
| Google Bilgi Paneli | Varlık tanıma |
| Wikipedia (eğer dikkat çekiciyse) | Otorite kaynağı |
| Web genelinde tutarlı bilgi | Varlık konsolidasyonu |
| Sektörel bahsedilmeler | Otorite sinyalleri |

---

## 7. YZ Tarayıcı Erişimi

### Temel YZ Kullanıcı Aracıları (User-Agents)

| Tarayıcı (Crawler) | Motor |
|---------|--------|
| GPTBot | ChatGPT/OpenAI |
| Claude-Web | Claude |
| PerplexityBot | Perplexity |
| Googlebot | Gemini (paylaşımlı) |

### Erişim Kararı

| Strateji | Ne Zaman Uygulanır? |
|----------|------|
| Hepsine izin ver | YZ alıntıları istendiğinde |
| GPTBot'u engelle | OpenAI eğitiminde kullanılmasını istemiyorsanız |
| Seçici erişim | Bazılarına izin ver, bazılarını engelle |

---

## 8. Ölçümleme

| Metrik | Nasıl Takip Edilir? |
|--------|--------------|
| YZ alıntıları | Manuel izleme |
| "[Marka Adı]'na göre" bahsedilmeleri | YZ içinde arama |
| Rakip alıntıları | Pazar payı karşılaştırması |
| YZ kaynaklı trafik | UTM parametreleri |

---

## 9. Anti-Desenler (Yapılmaması Gerekenler)

| ❌ YAPMAYIN | ✅ YAPIN |
|----------|-------|
| Tarih belirtmeden yayınlamak | Zaman damgaları ekleyin |
| Belirsiz atıflar yapmak | Kaynakları isimlendirin |
| Yazar bilgisini atlamak | Kimlik bilgilerini gösterin |
| Zayıf (thin) içerik | Kapsamlı kapsam sunun |

---

> **Unutmayın:** YZ; net, otoriter ve ayıklanması kolay içeriği alıntılar. Siz en iyi cevap olun.

---

## Script

| Script | Amaç | Komut |
|--------|---------|---------|
| `scripts/geo_checker.py` | GEO denetimi (YZ alıntı hazırlığı) | `python scripts/geo_checker.py <proje_yolu>` |
