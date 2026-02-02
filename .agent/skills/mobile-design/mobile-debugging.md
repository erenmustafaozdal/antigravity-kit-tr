# Mobil Hata Ayıklama (Debugging) Kılavuzu

> **console.log() ile hata ayıklamayı bırakın!**
> Mobil uygulamaların karmaşık native katmanları vardır. Metin logları yeterli değildir.
> **Bu dosya, etkili mobil hata ayıklama stratejilerini öğretir.**

---

## 🧠 MOBİL HATA AYIKLAMA ZİHNİYETİ

```
Web Hata Ayıklama:    Mobil Hata Ayıklama:
┌──────────────┐    ┌──────────────┐
│  Tarayıcı    │    │  JS Köprüsü  │
│  DevTools    │    │  Native UI   │
│  Network Tab │    │  GPU/Bellek  │
│  Thread'ler  │    │  Thread'ler  │
└──────────────┘    └──────────────┘
```

**Temel Farklar:**
1.  **Native Katmanı:** JS kodu çalışıyor ama uygulama çöküyor mu? Muhtemelen sorun native taraftadır (Java/Obj-C).
2.  **Dağıtım:** Sadece "sayfayı yenileyemezsiniz". Durum (state) kaybolabilir veya takılı kalabilir.
3.  **Ağ:** SSL Pinning ve proxy ayarları mobilde daha zordur.
4.  **Cihaz Logları:** `adb logcat` ve `Console.app` gerçekleri söyler.

---

## 🚫 YZ HATA AYIKLAMA ANTİ-DESENLERİ

| ❌ Varsayılan | ✅ Mobil-Doğru |
|------------|-------------------|
| "console.log ekle" | Flipper / Reactotron kullan |
| "Network tab'ı kontrol et" | Charles Proxy / Proxyman kullan |
| "Simülatörde çalışıyor" | **Gerçek Cihazda Test Et** (Donanıma özgü hatalar) |
| "node_modules'e sil yükle" | **Native Build'i Temizle** (Gradle/Pod cache) |
| Native logları yoksayma | `logcat` / Xcode loglarını oku |

---

## 1. Araç Seti

### ⚡ React Native & Expo

| Araç | Amaç | En İyi Kullanım |
|------|---------|----------|
| **Reactotron** | State/API/Redux | JS tarafı hata ayıklama |
| **Flipper** | Layout/Ağ/Veritabanı | Native + JS köprüsü |
| **Expo Araçları** | Element denetçisi | Hızlı UI kontrolleri |

### 🛠️ Native Katmanı (Derin Dalış)

| Araç | Platform | Komut | Neden Kullanılır? |
|------|----------|---------|----------|
| **Logcat** | Android | `adb logcat` | Native çökmeler, ANR'ler |
| **Console** | iOS | Xcode üzerinden | Native istisnalar, bellek |
| **Layout Insp.** | Android | Android Studio | UI hiyerarşi hataları |
| **View Insp.** | iOS | Xcode | UI hiyerarşi hataları |

---

## 2. Yaygın Hata Ayıklama İş Akışları

### 🕵️ "Uygulama Az Önce Çöktü" (Kırmızı Ekran vs Ana Ekrana Atma)

**Senaryo A: Kırmızı Ekran (JS Hatası)**
- **Neden:** `undefined is not an object`, import hatası vb.
- **Çözüm:** Ekrandaki stack trace'i (hata izini) okuyun. Genellikle nettir.

**Senaryo B: Ana Ekrana Atma (Native Çökme)**
- **Neden:** Native modül hatası, bellek yetersizliği (OOM), izinsiz özellik kullanımı.
- **Araçlar:**
    - **Android:** `adb logcat *:E` (Hataları filtrele)
    - **iOS:** Xcode → Window → Devices → View Device Logs

> **💡 İpucu:** Eğer uygulama açılır açılmaz çöküyorsa, %100 bir native yapılandırma sorunudur (Info.plist, AndroidManifest.xml).

---

## 3. Platforma Özgü Kabuslar

### Android
- **Gradle Senkronizasyon Hatası:** Genellikle Java versiyon uyumsuzluğu veya mükerrer sınıflar.
- **Emülatör Ağı:** Emülatör için `localhost` adresi `127.0.0.1` DEĞİL, `10.0.2.2`'dir.
- **Önbelleğe Alınmış Build'ler:** `./gradlew clean` komutu en iyi dostunuzdur.

### iOS
- **Pod Sorunları:** `pod deintegrate && pod install`.
- **İmzalama (Signing) Hataları:** Team ID ve Bundle Identifier'ı kontrol edin.
- **Önbellek:** Xcode → Product → Clean Build Folder.

---

## 📝 HATA AYIKLAMA KONTROL LİSTESİ

- [ ] **JS mi yoksa Native bir çökme mi?** (Kırmızı ekran mı yoksa ana ekran mı?)
- [ ] **Build'i temizlediniz mi?** (Native önbellekler çok agresiftir)
- [ ] **Gerçek bir cihazda mısınız?** (Simülatörler eşzamanlılık hatalarını gizler)
- [ ] **Native logları kontrol ettiniz mi?** (Sadece terminal çıktısına bakmayın)

---

> **Unutma:** Eğer JavaScript mükemmel görünüyorsa ama uygulama hala hata veriyorsa, Native tarafa daha yakından bakın.
