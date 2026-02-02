# Bağlam Keşfi (Context Discovery)

> Herhangi bir mimari önermeden önce bağlamı (context) toplayın.

## Soru Hiyerarşisi (ÖNCELİKLE Kullanıcıya Sorun)

1. **Ölçek (Scale)**
   - Kaç kullanıcı bekliyorsunuz? (10, 1K, 100K, 1M+)
   - Veri trafiği ne kadar? (MB, GB, TB)
   - İşlem hızı nedir? (Saniye/dakika başına işlem sayısı)

2. **Ekip (Team)**
   - Tek bir geliştirici mi yoksa bir ekip mi?
   - Ekip boyutu ve uzmanlık düzeyi nedir?
   - Dağıtık mı yoksa aynı lokasyonda mı çalışılıyor?

3. **Zaman Çizelgesi (Timeline)**
   - MVP/Prototipten mi bahsediyoruz yoksa uzun vadeli bir üründen mi?
   - Piyasaya çıkış süresi (time to market) baskısı var mı?

4. **Alan (Domain)**
   - CRUD ağırlıklı mı yoksa iş mantığı (business logic) karmaşık mı?
   - Gerçek zamanlı (real-time) çalışma gereksinimleri var mı?
   - Yasal uyumluluklar veya regülasyonlar (GDPR, KVKK vb.) geçerli mi?

5. **Kısıtlamalar (Constraints)**
   - Bütçe sınırlamaları var mı?
   - Entegre edilmesi gereken eski (legacy) sistemler var mı?
   - Teknoloji yığını (stack) tercihleri neler?

## Proje Sınıflandırma Matrisi

```
                    MVP              SaaS           Kurumsal (Enterprise)
┌─────────────────────────────────────────────────────────────┐
│ Ölçek        │ <1K           │ 1K-100K      │ 100K+        │
│ Ekip         │ Tek Kişi      │ 2-10         │ 10+          │
│ Zaman        │ Hızlı (Hafta) │ Orta (Ay)    │ Uzun (Yıl)   │
│ Mimari       │ Basit         │ Modüler      │ Dağıtık      │
│ Desenler     │ Minimal       │ Seçici       │ Kapsamlı     │
│ Örnek        │ Next.js API   │ NestJS       │ Mikroservis  │
└─────────────────────────────────────────────────────────────┘
```
