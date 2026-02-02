# Mobil Navigasyon Referansı

> Navigasyon desenleri, derin linkleme (deep linking), geri tuşu yönetimi ve tab/stack/drawer kararları.
> **Navigasyon uygulamanızın iskeletidir; yanlış yaparsanız her şey bozuk hissettirir.**

---

## 1. Navigasyon Seçimi Karar Ağacı

```
UYGULAMA TÜRÜ NEDİR?
        │
        ├── 3-5 ana bölüm (eşit öneme sahip)
        │   └── ✅ Tab Bar / Alt Navigasyon
        │       Örnekler: Sosyal Medya, E-ticaret, Araçlar
        │
        ├── Derin hiyerarşik içerik
        │   └── ✅ Stack (Yığın) Navigasyon
        │       Örnekler: Ayarlar, E-posta klasörleri
        │
        ├── Çok sayıda hedef (>5 ana bölüm)
        │   └── ✅ Drawer (Yan Menü) Navigasyon
        │       Örnekler: Gmail, karmaşık kurumsal uygulamalar
        │
        ├── Tekil doğrusal akış
        │   └── ✅ Sadece Stack (sihirbaz/onboarding)
        │       Örnekler: Ödeme adımları, kurulum akışı
        ```

---

## 2. Tab Bar Navigasyonu

### Ne Zaman Kullanılmalı?

```
✅ ŞU DURUMLARDA Tab Bar kullanın:
├── 3-5 ana hedef varsa
├── Hedefler eşit öneme sahipse
├── Kullanıcı bunlar arasında sık geçiş yapıyorsa
└── Her tab'ın bağımsız bir navigasyon yığını (stack) varsa

❌ ŞU DURUMLARDA Tab Bar'dan KAÇININ:
├── 5'ten fazla hedef varsa
├── Hedefler arasında net bir hiyerarşi varsa
└── İçerik bir dizi (sekans) halinde akıyorsa
```

### Tab Durumunun Korunması (State Preservation)

**KURAL:** Her tab kendi navigasyon yığınını korumasalıdır. Kullanıcı bir tab'da derinlere inip başka tab'a geçer ve geri dönerse, kaldığı yeri görmelidir (root sayfayı değil).

---

## 3. Stack (Yığın) Navigasyonu

### Temel Kavramlar
- **Push:** Üste yeni ekran ekle.
- **Pop:** Mevcut ekranı çıkar (geri git).
- **Replace:** Mevcut ekranı yenisiyle değiştir.
- **Reset:** Yığını temizle ve yeni bir başlangıç (root) belirle.

### Geri Tuşu Yönetimi
- **iOS:** Kenardan sağa kaydırma (edge swipe) yereldir ve her zaman çalışmalıdır.
- **Android:** Sistem geri tuşu/jesti her zaman yığını geri götürmelidir.

---

## 4. Modal Navigasyon

### Modal vs Push

```
PUSH (Stack):                    MODAL:
├── Yatay kayma (iOS)            ├── Dikey yukarı açılma (sheet)
├── Hiyerarşinin parçası         ├── Ayrı bir görev
├── Geri tuşu ile döner          ├── Kapatma (X) butonu ile döner
└── "Derine inme"                └── "Göreve odaklanma"

ŞUNLAR İÇİN MODAL KULLANIN:
├── Yeni içerik oluşturma
├── Ayarlar / Tercihler
├── Bir işlemi tamamlama (Transaction)
├── Hızlı eylemler
```

---

## 5. Derin Linkleme (Deep Linking)

### Neden İlk Günden Planlanmalı?
- Push bildirimleri ile navigasyon.
- İçerik paylaşımı.
- Pazarlama kampanyaları.
- Widget navigasyonu.

### Navigasyon Kuralları
1. **Tam Yığın İnşası:** Bir derin linke tıklandığında (örn: `myapp://product/123`), yığın doğru kurulmalıdır (Ana sayfa altta, ürün üstte).
2. **Kimlik Doğrulama:** Link auth gerektiriyorsa, önce login'e yönlendirip sonra hedefe gitmelidir.
3. **Geçersiz Linkler:** Hatalı linklerde uygulama çökmemeli, ana sayfaya yönlendirip hata mesajı göstermelidir.

---

## 6. Navigasyon Geçiş Animasyonları

### Platform Varsayılanları
- **iOS:** Sağdan sola kayma (Push), alttan yukarı açılma (Modal).
- **Android:** Hafif solma + sağdan kayma (Push), alttan yukarı açılma (Modal).

### Shared Element (Paylaşılan Öğe) Geçişleri
İki ekran arasındaki ortak öğeyi (örn: listedeki resmin detay sayfasında büyümesi) anime ederek devamlılık hissi sağlar.

---

## 7. Navigasyon Anti-Desenleri

- **Tutarsız Geri Tuşu:** Kullanıcının nereye döneceğini tahmin edememesi.
- **Gizli Navigasyon:** Özelliklerin keşfedilememesi (Drawer içinde saklı kalması).
- **Derin İç İçe Yapı:** 3-4 seviyeden fazla derinlik kullanıcıyı kaybettirir.
- **Geri Kaydırmayı Bozma:** iOS'ta edge swipe jestini iptal etmek kullanıcıyı hüsrana uğratır.

---

## 8. Navigasyon Kontrol Listesi

- [ ] **Uygulama türüne göre navigasyon yapısı seçildi mi?**
- [ ] **Derin link (URL scheme) planlandı mı?**
- [ ] **Tab durumları (state) korunuyor mu?**
- [ ] **iOS'ta edge swipe çalışıyor mu?**
- [ ] **Android 14+ Predictive Back destekleniyor mu?**
- [ ] **Push bildirimleri ile derin link navigasyonu çalışıyor mu?**

---

> **Unutma:** Navigasyon doğru yapıldığında görünmezdir. Kullanıcılar bir yere NASIL gideceklerini düşünmemeli—sadece oraya varmalıdırlar. Eğer navigasyonu fark ediyorlarsa, bir şeyler ters gidiyor demektir.
