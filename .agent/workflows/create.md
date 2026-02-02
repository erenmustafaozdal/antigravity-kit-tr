---
description: Yeni uygulama oluşturma komutu. App Builder yeteneğini tetikler ve kullanıcıyla etkileşimli bir diyalog başlatır.
---

# /create - Uygulama Oluştur

$ARGUMENTS

---

## Görev

Bu komut, yeni bir uygulama oluşturma sürecini başlatır.

### Adımlar:

1. **İstek Analizi**
   - Kullanıcının ne istediğini anla
   - Eksik bilgi varsa, sormak için `conversation-manager` yeteneğini kullan

2. **Proje Planlama**
   - Görev kırılımı için `project-planner` ajanını kullan
   - Teknoloji yığınını belirle
   - Dosya yapısını planla
   - Plan dosyasını oluştur ve oluşturma aşamasına geç

3. **Uygulama Oluşturma (Onaydan Sonra)**
   - `app-builder` yeteneği ile orkestre et
   - Uzman ajanları koordine et:
     - `database-architect` → Şema
     - `backend-specialist` → API
     - `frontend-specialist` → UI

4. **Önizleme**
   - Tamamlandığında `auto_preview.py` ile başlat
   - URL'yi kullanıcıya sun

---

## Kullanım Örnekleri

```
/create blog sitesi
/create ürün listeleme ve sepet içeren e-ticaret uygulaması
/create yapılacaklar (todo) uygulaması
/create Instagram klonu
/create müşteri yönetimi içeren crm sistemi
```

---

## Başlamadan Önce

İstek net değilse şu soruları sor:
- Ne tür bir uygulama?
- Temel özellikler nelerdir?
- Kimler kullanacak?

Varsayılanları kullan, ayrıntıları daha sonra ekle.
