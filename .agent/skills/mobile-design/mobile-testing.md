# Mobil Test Desenleri

> **Mobil test, web testi değildir. Farklı kısıtlamalar, farklı stratejiler.**
> Bu dosya, her bir test yaklaşımının NE ZAMAN ve NEDEN kullanılacağını öğretir.
> **Kod örnekleri minimaldir - karar verme sürecine odaklanın.**

---

## 🧠 MOBİL TEST ZİHNİYETİ

```
Mobil testin webden farkları:
├── Gerçek cihazlar önemlidir (emülatörler hataları gizler)
├── Platform farklılıkları (iOS vs Android davranışı)
├── Ağ koşulları çılgınca değişir
├── Test altında pil/performans durumu
├── Uygulama yaşam döngüsü (arka plan, sonlandırma, geri yükleme)
├── İzinler ve sistem diyalogları
├── Tıklama yerine dokunmatik etkileşimler
```

---

## 🚫 YZ MOBİL TEST ANTİ-DESENLERİ

| ❌ YZ Varsayılanı | Neden Yanlış? | ✅ Mobil-Doğru |
|---------------|----------------|-------------------|
| Sadece Jest testleri | Native katmanı kaçırır | Jest + Cihazda E2E |
| Enzyme desenleri | Eskidi, web odaklı | React Native Testing Library |
| Tarayıcı tabanlı E2E (Cypress) | Native özellikleri test edemez | Detox / Maestro |
| Her şeyi mock'lamak | Entegrasyon hatalarını kaçırır | Gerçek cihaz testi |
| Platform testlerini yoksay | iOS/Android farklıdır | Platforma özgü durumlar |
| Performans testlerini atla | Mobilde performans kritiktir | Düşük segment cihazda profil çıkar |
| Sadece mutlu yolu test et | Mobilde uç durumlar (edge case) fazladır | Çevrimdışı, izinler, kesintiler |

---

## 1. Test Aracı Seçimi

### Karar Ağacı

```
NEYİ TEST EDİYORSUNUZ?
        │
        ├── Saf fonksiyonlar, yardımcı araçlar (utilities)
        │   └── Jest (birim testler)
        │
        ├── Tekil bileşenler (izole edilmiş)
        │   ├── React Native → React Native Testing Library
        │   └── Flutter → flutter_test (widget testleri)
        │
        ├── Hooklar, context ve navigasyon içeren bileşenler
        │   ├── React Native → RNTL + mock'lanmış provider'lar
        │   └── Flutter → integration_test paketi
        │
        ├── Tam kullanıcı akışları (login, ödeme vb.)
        │   ├── Detox (React Native, hızlı, güvenilir)
        │   ├── Maestro (Cross-platform, YAML tabanlı)
        │   └── Appium (Eski, yavaş, son çare)
        │
        └── Performans, bellek, pil
            ├── Flashlight (RN performansı)
            ├── Flutter DevTools
            └── Gerçek cihaz profili (Xcode/Android Studio)
```

---

## 2. Mobil İçin Test Piramidi

```
                    ┌───────────────┐
                    │    E2E Testler│  %10
                    │(Gerçek Cihaz) │  Yavaş, maliyetli, vazgeçilmez
                    ├───────────────┤
                    │ Entegrasyon   │  %20
                    │    Testleri   │  Bileşen + bağlam (context)
                    ├───────────────┤
                    │   Bileşen     │  %30
                    │   Testleri    │  İzole edilmiş UI
                    ├───────────────┤
                    │   Birim (Unit)│  %40
                    │    Testleri   │  Saf mantık
                    └───────────────┘
```

> 🔴 **Eğer %90 birim testiniz ve %0 E2E testiniz varsa, yanlış şeyleri test ediyorsunuz demektir.**

---

## 3. Platforma Özgü Testler

| Alan | iOS Davranışı | Android Davranışı | İkisinde de mi? |
|------|--------------|------------------|------------|
| **Geri Navigasyon** | Kenardan kaydırma | Sistem geri butonu | ✅ EVET |
| **İzinler** | Bir kere sor, ayarlara at | Her seferinde sor, açıklama sun | ✅ EVET |
| **Klavye** | Farklı görünüm | Farklı davranış | ✅ EVET |
| **Deep Linkler** | Universal Links | App Links | ✅ EVET |

---

## 4. Çevrimdışı ve Ağ Testleri

| Senaryo | Neyi Doğrulamalı? |
|----------|----------------|
| Çevrimdışı başlatma | Önbellekteki veri veya mesajı gösterir |
| Eylem sırasında kesinti | Eylem kuyruğa alınır, kaybolmaz |
| Çevrimdışı → Çevrimiçi | Kuyruk senkronize olur, mükerrer kayıt oluşmaz |
| Yavaş ağ (2G) | Yükleme durumları, zaman aşımları çalışır |

---

## 5. Erişilebilirlik (Accessibility) Testleri

- [ ] **Tüm etkileşimli öğeler `accessibilityLabel` içeriyor mu?**
- [ ] **Görsellerin alt metni var mı?**
- [ ] **Botonların rolü (`button`) tanımlanmış mı?**
- [ ] **Dokunmatik hedefler ≥ 44x44 (iOS) / 48x48 (Android) mi?**
- [ ] **Renk kontrastı WCAG AA seviyesinde mi?**

---

## 📝 MOBİL TEST KONTROL LİSTESİ

- [ ] **Yeni mantık için birim testleri hazır mı?**
- [ ] **Yeni UI için bileşen testleri hazır mı?**
- [ ] **Gerçek iOS ve Android cihazda E2E testi yapıldı mı?**
- [ ] **Düşük segment cihazda test edildi mi?**
- [ ] **Çevrimdışı senaryolar doğrulandı mı?**
- [ ] **Performans kabul edilebilir seviyede mi?**
- [ ] **Erişilebilirlik doğrulandı mı?**

---

> **Unutma:** İyi mobil test stratejisi HER ŞEYİ değil, DOĞRU şeyleri test etmekle ilgilidir. Kararsız (flaky) bir E2E testi, hiç test olmamasından daha kötüdür. Bir hatayı yakalayan başarısız bir birim testi, 100 tane geçen önemsiz testten daha değerlidir.
