---
description: Mevcut uygulamaya özellikler ekleyin veya bunları güncelleyin. Yinelemeli (iterative) geliştirme için kullanılır.
---

# /enhance - Uygulamayı Güncelle/İyileştir

$ARGUMENTS

---

## Görev

Bu komut, mevcut uygulamaya yeni özellikler ekler veya mevcut özellikleri günceller.

### Adımlar:

1. **Mevcut Durumu Anla**
   - Proje durumunu `python .agent/scripts/session_manager.py info` ile yükle
   - Mevcut özellikleri ve teknoloji yığınını anla

2. **Değişiklikleri Planla**
   - Nelerin ekleneceğini/değiştirileceğini belirle
   - Etkilenen dosyaları tespit et
   - Bağımlılıkları kontrol et

3. **Planı Kullanıcıya Sun** (büyük değişiklikler için)
   ```
   "Yönetim paneli eklemek için:
   - 15 yeni dosya oluşturacağım
   - 8 dosyayı güncelleyeceğim
   - Yaklaşık 10 dakika sürecek
   
   Başlayayım mı?"
   ```

4. **Uygula**
   - İlgili ajanları çağır
   - Değişiklikleri yap
   - Test et

5. **Önizlemeyi Güncelle**
   - Hot reload yap veya yeniden başlat

---

## Kullanım Örnekleri

```
/enhance karanlık mod ekle
/enhance yönetim paneli oluştur
/enhance ödeme sistemi entegre et
/enhance arama özelliği ekle
/enhance profil sayfasını düzenle
/enhance duyarlı (responsive) yap
```

---

## Dikkat

- Büyük değişiklikler için onay al
- Çelişkili istekler konusunda uyar (örneğin, proje PostgreSQL kullanırken "Firebase kullan" denmesi)
- Her değişikliği git ile commit'le
