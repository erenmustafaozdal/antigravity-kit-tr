---
description: project-planner ajanını kullanarak proje planı oluşturun. Kod yazımı yoktur - sadece plan dosyası oluşturulur.
---

# /plan - Proje Planlama Modu

$ARGUMENTS

---

## 🔴 KRİTİK KURALLAR

1. **KOD YAZIMI YOK** - Bu komut sadece plan dosyası oluşturur
2. **project-planner ajanını kullan** - Antigravity Ajanının yerel Plan modunu DEĞİL
3. **Sokratik Geçit** - Planlamadan önce açıklayıcı sorular sor
4. **Dinamik İsimlendirme** - Plan dosyası göreve göre isimlendirilir

---

## Görev

`project-planner` ajanını bu bağlamla kullanın:

```
BAĞLAM:
- Kullanıcı İsteği: $ARGUMENTS
- Mod: SADECE PLANLAMA (kod yok)
- Çıktı: docs/PLAN-{gorev-slug}.md (dinamik isimlendirme)

İSİMLENDİRME KURALLARI:
1. İstekten 2-3 anahtar kelime seç
2. Küçük harf, tire ile ayrılmış
3. Maksimum 30 karakter
4. Örnek: "e-ticaret sepeti" → PLAN-eticaret-sepeti.md

KURALLAR:
1. project-planner.md Aşama -1'i takip et (Bağlam Kontrolü)
2. project-planner.md Aşama 0'ı takip et (Sokratik Geçit)
3. Görev kırılımı içeren PLAN-{slug}.md dosyasını oluştur
4. Herhangi bir kod dosyası YAZMA
5. Oluşturulan tam dosya adını BİLDİR
```

---

## Beklenen Çıktı

| Çıktı | Konum |
|-------------|----------|
| Proje Planı | `docs/PLAN-{gorev-slug}.md` |
| Görev Kırılımı | Plan dosyası içinde |
| Ajan Atamaları | Plan dosyası içinde |
| Doğrulama Listesi | Plan dosyasındaki Aşama X |

---

## Planlamadan Sonra

Kullanıcıya söyle:
```
[TAMAM] Plan oluşturuldu: docs/PLAN-{slug}.md

Sonraki adımlar:
- Planı inceleyin
- Uygulamaya başlamak için `/create` komutunu çalıştırın
- Veya planı manuel olarak düzenleyin
```

---

## İsimlendirme Örnekleri

| İstek | Plan Dosyası |
|---------|-----------|
| `/plan sepetli e-ticaret sitesi` | `docs/PLAN-eticaret-sepeti.md` |
| `/plan fitness için mobil uygulama` | `docs/PLAN-fitness-uygulamasi.md` |
| `/plan karanlık mod özelliği ekle` | `docs/PLAN-karanlik-mod.md` |
| `/plan kimlik doğrulama hatasını çöz` | `docs/PLAN-auth-cozum.md` |
| `/plan SaaS paneli` | `docs/PLAN-saas-paneli.md` |

---

## Kullanım

```
/plan sepetli e-ticaret sitesi
/plan fitness takip mobil uygulaması
/plan analitik içeren SaaS paneli
```
