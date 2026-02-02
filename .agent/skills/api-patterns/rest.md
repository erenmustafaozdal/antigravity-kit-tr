# REST Prensipleri

> Kaynak tabanlı API tasarımı - fiiller değil, isimler.

## Kaynak İsimlendirme Kuralları

```
Prensipler:
├── Fiil değil, İSİMLERİ kullanın (eylemler değil, kaynaklar)
├── ÇOĞUL formlar kullanın (/user değil, /users)
├── Küçük harf ve kısa çizgi kullanın (/user-profiles)
├── İlişkiler için iç içe yapı kullanın (/users/123/posts)
└── Derinliği sınırlı tutun (maksimum 3 seviye)
```

## HTTP Metot Seçimi

| Metot | Amaç | Idempotent (Eşgüçlü)? | Body? |
|--------|---------|-------------|-------|
| **GET** | Kaynak(ları) oku | Evet | Hayır |
| **POST** | Yeni kaynak oluştur | Hayır | Evet |
| **PUT** | Kaynağı tamamen değiştir | Evet | Evet |
| **PATCH** | Kısmi güncelleme | Hayır | Evet |
| **DELETE** | Kaynağı sil | Evet | Hayır |

## Durum Kodu (Status Code) Seçimi

| Durum | Kod | Neden |
|-----------|------|-----|
| Başarılı (okuma) | 200 | Standart başarı |
| Oluşturuldu | 201 | Yeni kaynak başarıyla oluşturuldu |
| İçerik yok | 204 | Başarılı, ancak dönecek içerik yok |
| Hatalı istek | 400 | Biçimi bozuk veya geçersiz istek |
| Yetkisiz | 401 | Eksik veya geçersiz kimlik bilgisi (Auth) |
| Yasaklandı | 403 | Geçerli auth, ancak işlem yetkisi yok |
| Bulunamadı | 404 | Kaynak mevcut değil |
| Çakışma | 409 | Durum çakışması (örneğin mükerrer kayıt) |
| Doğrulama hatası | 422 | Geçerli sözdizimi, ancak geçersiz veri |
| İstek sınırı | 429 | Çok fazla istek (Rate limited) |
| Sunucu hatası | 500 | Sunucu taraflı bir hata oluştu |
