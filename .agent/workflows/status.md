---
description: Ajan ve proje durumunu görüntüler. İlerleme takibi ve durum panosu.
---

# /status - Durumu Göster

$ARGUMENTS

---

## Görev

Mevcut proje ve ajan durumunu gösterir.

### Neler Gösterilir?

1. **Proje Bilgisi**
   - Proje adı ve yolu
   - Teknoloji yığını
   - Mevcut özellikler

2. **Ajan Durum Panosu**
   - Hangi ajanlar çalışıyor
   - Hangi görevler tamamlandı
   - Bekleyen işler

3. **Dosya İstatistikleri**
   - Oluşturulan dosya sayısı
   - Değiştirilen dosya sayısı

4. **Önizleme Durumu**
   - Sunucu çalışıyor mu?
   - URL
   - Sağlık kontrolü (health check)

---

## Örnek Çıktı

```
=== Proje Durumu ===

📁 Proje: my-ecommerce
📂 Yol: C:/projects/my-ecommerce
🏷️ Tür: nextjs-ecommerce
📊 Durum: aktif

🔧 Teknoloji Yığını:
   Framework: next.js
   Veritabanı: postgresql
   Kimlik Doğrulama: clerk
   Ödeme: stripe

✅ Özellikler (5):
   • ürün-listeleme
   • sepet
   • ödeme-sayfasi
   • kullanıcı-auth
   • sipariş-gecmisi

⏳ Bekleyenler (2):
   • admin-paneli
   • e-posta-bildirimleri

📄 Dosyalar: 73 oluşturuldu, 12 değiştirildi

=== Ajan Durumu ===

✅ database-architect → Tamamlandı
✅ backend-specialist → Tamamlandı
🔄 frontend-specialist → Dashboard bileşenleri (%60)
⏳ test-engineer → Bekliyor

=== Önizleme ===

🌐 URL: http://localhost:3000
💚 Sağlık: TAMAM (OK)
```

---

## Teknik Bilgi

Durum bilgisi şu scriptleri kullanır:
- `python .agent/scripts/session_manager.py status`
- `python .agent/scripts/auto_preview.py status`
