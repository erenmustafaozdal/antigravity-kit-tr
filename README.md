# Antigravity Kit (TR Core)

> Yetenekler, Ajanlar ve İş Akışları ile YZ Ajan Şablonları

## Hızlı Kurulum

Bu versiyon, doğrudan projenize klonlanarak kullanılmak üzere tasarlanmıştır. Projenize eklemek için:

```bash
git clone https://github.com/erenmustafaozdal/antigravity-kit-tr .agent
```

Bu komut tüm şablonları içeren `.agent` klasörünü projenize indirir. Eğer bir Git projesi içindeyseniz, `.gitignore` dosyanıza `.agent/` eklemeyi unutmayın.

## Neler Dahil?

| Bileşen       | Sayı | Açıklama                                                           |
| ------------- | ---- | ------------------------------------------------------------------ |
| **Ajanlar**   | 20   | Uzman YZ personaları (frontend, backend, güvenlik, PM, QA vb.)     |
| **Yetenekler**| 36   | Alan-bazlı bilgi modülleri                                         |
| **İş Akışları**| 11   | Slash komutu prosedürleri                                          |


## Kullanım

### Ajanları Kullanma

**Ajanları açıkça belirtmenize gerek yok!** Sistem otomatik olarak doğru uzmanı/uzmanları algılar ve uygular:

```
Siz: "JWT kimlik doğrulama ekle"
YZ: 🤖 @security-auditor + @backend-specialist uygulanıyor...

Siz: "Karanlık mod butonunu düzelt"
YZ: 🤖 @frontend-specialist kullanılıyor...

Siz: "Giriş 500 hatası veriyor"
YZ: 🤖 Sistematik analiz için @debugger kullanılıyor...
```

**Nasıl Çalışır:**

- İsteğinizi sessizce analiz eder
- Alan(lar)ı otomatik algılar (frontend, backend, güvenlik vb.)
- En iyi uzman(lar)ı seçer
- Hangi uzmanlığın uygulandığını size bildirir
- Sistem mimarisini bilmenize gerek kalmadan uzman düzeyinde yanıtlar alırsınız

**Avantajlar:**

- ✅ Öğrenme eğrisi yok - sadece neye ihtiyacınız olduğunu tarif edin
- ✅ Her zaman uzman yanıtları alın
- ✅ Şeffaf - hangi ajanın kullanıldığını gösterir
- ✅ İsterseniz ajanı açıkça belirterek geçersiz kılabilirsiniz

### İş Akışlarını Kullanma

İş akışlarını slash komutları ile çağırın:

| Komut            | Açıklama                              |
| ---------------- | ------------------------------------- |
| `/brainstorm`    | Uygulamadan önce seçenekleri keşfet   |
| `/create`        | Yeni özellikler veya uygulamalar yarat|
| `/debug`         | Sistematik hata ayıklama              |
| `/deploy`        | Uygulamayı dağıt                      |
| `/enhance`       | Mevcut kodu iyileştir                 |
| `/orchestrate`   | Çoklu-ajan koordinasyonu              |
| `/plan`          | Görev kırılımı oluştur                |
| `/preview`       | Değişiklikleri yerel olarak önizle    |
| `/status`        | Proje durumunu kontrol et             |
| `/test`          | Test üret ve çalıştır                 |
| `/ui-ux-pro-max` | 50 stil ile tasarım yap               |

Örnek:

```
/brainstorm kimlik doğrulama sistemi
/create hero bölümü olan bir landing page
/debug giriş neden başarısız oluyor
```

### Yetenekleri Kullanma

Yetenekler, görev bağlamına göre otomatik olarak yüklenir. YZ, yetenek açıklamalarını okur ve ilgili bilgiyi uygular.

## Dokümantasyon

- **[Web Uygulaması Örneği](https://antigravity-kit.vercel.app//docs/guide/examples/web-app)** - Web uygulaması oluşturma rehberi (*İngilizce*)
- **[Online Dokümanlar](https://antigravity-kit.vercel.app//docs)** - Tüm dokümantasyonu çevrimiçi inceleyin (*İngilizce*)

## Lisans

MIT © Vudovn (Original), Eren Mustafa Özdal (TR Fork)
