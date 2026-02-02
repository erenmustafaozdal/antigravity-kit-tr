# Mobil Karar Ağaçları

> Framework seçimi, state yönetimi, depolama stratejisi ve bağlama dayalı kararlar.
> **Bunlar DÜŞÜNME rehberleridir, kopyala-yapıştır cevaplar değildir.**

---

## 1. Framework Seçimi

### Ana Karar Ağacı

```
NE İNŞA EDİYORSUNUZ?
        │
        ├── App Store onayı beklemeden OTA (anlık) güncelleme lazım mı?
        │   │
        │   ├── Evet → React Native + Expo
        │   │         ├── Geliştirme için Expo Go
        │   │         ├── Prodüksiyon güncellemeleri için EAS Update
        │   │         └── En iyisi: Hızlı iterasyon, web ekipleri
        │   │
        │   └── Hayır → Devam et ▼
        │
        ├── Platformlar arası mükemmel (pixel-perfect) özel UI lazım mı?
        │   │
        │   ├── Evet → Flutter
        │   │         ├── Kendi render motoru
        │   │         ├── iOS + Android için tekil UI
        │   │         └── En iyisi: Marka odaklı, görsel uygulamalar
        │   │
        │   └── Hayır → Devam et ▼
        │
        ├── Yoğun native özellikler (ARKit, HealthKit, özel sensörler) mi var?
        │   │
        │   ├── Sadece iOS → SwiftUI / UIKit
        │   ├── Sadece Android → Kotlin + Jetpack Compose
        │   └── Her ikisi → Kotlin Multiplatform (KMP) değerlendir
```

---

## 2. State Yönetimi Seçimi

### React Native İçin
- **Basit uygulama:** Zustand (veya Context).
- **Sunucu verisi ağırlıklı:** TanStack Query (React Query) + Zustand.
- **Karmaşık/Büyük ölçekli:** Redux Toolkit + RTK Query.
- **Atomik yapı:** Jotai.

### Flutter İçin
- **Öğrenme aşaması:** Provider.
- **Modern ve tip güvenli:** Riverpod 2.0.
- **Kesin kurallar ve kurumsal:** BLoC.

---

## 3. Depolama Stratejisi Seçimi

```
VERİ TÜRÜ NEDİR?
        │
        ├── Hassas (tokenlar, şifreler, anahtarlar)
        │   └── ✅ Güvenli Depolama (Keychain / SecureStore)
        │
        ├── Kullanıcı tercihleri (ayarlar, tema)
        │   └── ✅ Key-Value Depolama (MMKV / AsyncStorage / SharedPreferences)
        │
        ├── Yapılandırılmış veriler (ilişkisel tablolar)
        │   └── ✅ Veritabanı (SQLite / WatermelonDB / Realm)
        │
        ├── Büyük dosyalar (görseller, dokümanlar)
        │   └── ✅ Dosya Sistemi (File System)
        │
        └── Önbelleğe alınmış API verileri
            └── ✅ Sorgu Kütüphanesi Önbelleği (TanStack Query / Riverpod)
```

---

## 4. Çevrimdışı (Offline) Stratejisi

1. **Önbellek-Öncelikli (Basit):** Önce önbelleğe bak, eskiyse ağdan çek.
2. **Stale-While-Revalidate:** Önbelleği hemen göster, arka planda ağdan güncelle.
3. **Önce-Çevrimdışı (Karmaşık):** Yerel veritabanı "tek gerçeklik" kaynağıdır; değişiklikler kuyruğa alınır ve online olunca senkronize edilir.

---

## 5. Uygulama Tipi Şablonları

- **E-Ticaret:** React Native + Expo (OTA için), Tab Bar, TanStack Query.
- **Sosyal Medya:** React Native veya Flutter, Tab Bar, SQLite (akış önbelleği), WebSocket.
- **SaaS / Verimlilik:** Flutter (tutarlı UI), BLoC veya Riverpod, Tam çevrimdışı düzenleme desteği.

---

## 6. Karar Kontrol Listesi

- [ ] **Hedef platformlar belirlendi mi (iOS/Android)?**
- [ ] **Kriterlere göre framework seçildi mi?**
- [ ] **State yönetimi projenin ölçeğine uygun mu?**
- [ ] **Hassas veriler için güvenli depolama seçildi mi?**
- [ ] **Derin linkleme (deep linking) planlandı mı?**
- [ ] **Çevrimdışı gereksinimler net mi?**

---

> **Unutma:** Bu ağaçlar DÜŞÜNME için birer rehberdir, körü körüne izlenecek kurallar değildir. Her projenin kendine has kısıtlamaları vardır. Gereksinimler belirsiz olduğunda netleştirici sorular sorun ve varsayılanlara değil, gerçek ihtiyaçlara göre seçim yapın.
